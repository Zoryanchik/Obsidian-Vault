```java
//declared globally
//connect to database
const dbname = "lab8"
const db = connect( "mongodb://localhost/" + dbname );

// Provided function
// Reads album json data and runs function on each album object.
function importAlbums(filename) {
	// Drop any existing data, so do not repeat duplicate data.
	db.songs.drop();
	db.albums.drop();

	// Parse file into album objects array
	const albums = JSON.parse(fs.readFileSync(filename));

	// Loop through each album object and process with addAlbum function
	albums.forEach(addAlbum);
}


// Provided function
// To be updated in Task 2
function addAlbum(album) {
	console.log("Adding " + album.title);
	// Insert all tracks into songs, and retain added ids
	const added = db.songs.insertMany(album.tracks);
	const track_ids = Object.values(added.insertedIds);
	
	// Replace the tracks array (song objects) in the album object, with an array of song ids.
	// For Task 2, create and use an array of song objects with required fields, from the songs collection (toArray()).

	// Get _id, title and duration from songs in track_ids, converted to array.
	const tracks_d = db.songs.find({"_id" : {$in : track_ids}},{"title":1, "duration":1}).toArray();

	// Update album.tracks array with newly created array.
	album.tracks = tracks_d

	// Insert the album object as a document in albums.
	db.albums.insertOne(album);
}


// Function to be completed for logging plays, in Tasks 4, 5 & 6.
// year and month variables provided, calculated from timestamp.
function logPlay(username, song_id, timestamp = new Date()) {
	const year = timestamp.getFullYear();
	const month = timestamp.getMonth()+1; // months starts at 0, hence +1.


	// Task 4 code here
	// The bucket to be updated is defined by the query: user, year, month.
	// The timestamp and song_id are added to the plays array in this bucket, and the count field is incremented.
	// upsert: true means that the bucket will be created if there isn't already one for the user, year, month combination.
	// The size of the buckets could be limited by including the count in the query part.
	db.plays.updateOne(	{	"user": username,
							"year":  year,
							"month": month },
						{ $push: { "plays" : { "ts": timestamp, "song": song_id } },
						  $inc: {"count": 1 }
						},
						{ "upsert": true }
	);

	// Task 5 code here
	// Get the song details
	const song = db.songs.findOne({"_id" : song_id},{"_id": 0, "title": 1, "artist": 1});
	// Add timestamp to song object.
	song.timestamp = timestamp;


	// Add song to recent plays array, limiting size to 20, and sorting descending by timestamp
	db.users.updateOne(
		{"username" : username},
		{
			$push : {
				"recent_plays": {
					$each: [song],
					$sort : {"timestamp" : -1},
					$slice: 20
				}
			}
		}
	);


	// Task 6.1 code here (or incorporate into Task 4 & 5 code above)

	// Increment total_plays in songs by 1.
	// This could be included in Task 5, by including in users update.
	db.users.updateOne({"username" : username}, 
							{$inc : {"total_plays": 1}}
						);

	// Increment total_plays in songs by 1.
	// This could be included in Task 5, by using findOneAndUpdate() instead of findOne.
	db.songs.updateOne({"_id": song_id}, {$inc: {"total_plays": 1}});

	// Task 6.2 code here.
	// Increment total_plays in song, if song_id found in tracks array's _id fields.
	db.albums.updateOne({"tracks._id" : song_id}, {$inc: {"total_plays": 1}})
}


// Provided function
// Uses logPlay function to add songs randomly selected from song_ids array, 
// with a timestamp at a random number of days in past.
// Repeated n times.
function addRandomPlays(username, song_ids, n) {
	for(let i = 0; i<n; i++) {
		const random_song_index = Math.floor(Math.random() * song_ids.length);
		const random_days = Math.floor(Math.random() * 730);
		const ts = new Date();
		ts.setDate(ts.getDate() - random_days);
		logPlay(username, song_ids[random_song_index], ts);
	}
}
```
![[Pasted image 20260106013035.png]]![[Pasted image 20260106013058.png]]![[Pasted image 20260106013114.png]]