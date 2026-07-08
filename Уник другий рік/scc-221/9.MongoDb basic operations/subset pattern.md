![[Pasted image 20260105224557.png]]![[Pasted image 20260105224604.png]]![[Pasted image 20260105224647.png]]![[Pasted image 20260105224728.png]]### Phase 1: Preparation & Archiving
The goal of this code is to maintain a short list of **"Recently Played"** songs inside the User document, while keeping the full history in a separate collection. This keeps the User document small and fast to load.
The first part of the function handles the data setup and permanent logging.

JavaScript

```java
const timestamp = new Date();
db.plays.insertOne({ "ts": timestamp, "user": user_id, "song": song_id }); 
```

- **Timestamp:** It creates a current timestamp so we know exactly when the song was played.
    
- **The "Master" Log:** It inserts a record into a `plays` collection. This collection will grow indefinitely, containing the history of _every song ever played_ by _every user_. This is where the full data lives, but it is slow to query frequently.
    

### Phase 2: Fetching Details

JavaScript

```java
const song = db.songs.findOne({ "_id": song_id });
const play_d = { 
    "song_id": song_id, 
    "title": song.title, 
    "artist": song.artist, 
    "timestamp": timestamp 
};
```

- **Fetch Song Info:** It retrieves the song's title and artist from the `songs` collection.
    
- **Create the Subset:** It creates a small object (`play_d`) containing only the essential data needed for a UI display (like a "Recent Plays" widget). This avoids storing unnecessary data (like lyrics) in the user's profile.
    

### Phase 3: The "Smart" Update (The Key Part)

This is where the magic happens. The code updates the `users` collection to add this new play to their profile.

JavaScript
"Go into the `users` collection. Ignore everyone else. Find the **one specific document** where the `_id` field matches the value inside my `user_id` variable.
```java
db.users.updateOne(
  { "_id": user_id },
  { 
    $push: {
      "recent_plays": {
        $each: [play_d],           // 1. Add the new song
        $sort: { "timestamp": -1 }, // 2. Sort the list (Newest first)
        $slice: 5                   // 3. Keep only the top 5
      }
    }
  }
);
```

This single `$push` command does three things at once using **modifiers**:

1. **`$each: [play_d]`**: This prepares the new item to be added. You must use `$each` if you want to use the other modifiers (`$sort` or `$slice`), even if you are only adding one item.
    
2. **`$sort: { "timestamp": -1 }`**: After adding the new song, it re-sorts the entire `recent_plays` array by timestamp in **descending order** (-1). This ensures the newest songs are always at the start of the array.
    
3. **`$slice: 5`**: This trims the array. It tells MongoDB, "After sorting, only keep the first 5 items and delete the rest." This ensures the array never grows beyond 5 items, preventing the User document from becoming infinitely large.

```java
function logPlay(user_id, song_id) {
    // 1. CREATE TIMESTAMP
    // We capture the exact moment the song was played.
    const timestamp = new Date();

    // 2. WRITE TO THE "MASTER LOG" (The Infinite History)
    // We insert a record into the main 'plays' collection.
    // This collection grows forever and stores every single play event
    // for analytics, but it is too slow to query for a simple profile page.
    db.plays.insertOne({ "ts": timestamp, "user": user_id, "song": song_id });

    // 3. FETCH SONG DETAILS
    // We look up the song title and artist from the 'songs' collection
    // because the 'logPlay' function was only given the 'song_id'.
    const song = db.songs.findOne({ "_id" : song_id });

    // 4. PREPARE THE SUBSET DATA
    // We create a small object with ONLY the info needed for the UI.
    // We don't include heavy data (like lyrics) here to save space.
    const play_d = {
        "song_id": song_id,
        "title" : song.title,
        "artist": song.artist,
        "timestamp": timestamp
    };

    // 5. UPDATE THE USER PROFILE (The "Smart" Update)
    db.users.updateOne(
        { "_id" : user_id }, // Find the user who just played the song
        {
            $push : {
                "recent_plays": {
                    // $each: This is required when using modifiers like $sort or $slice.
                    // It treats 'play_d' as a list of items to be added.
                    $each: [play_d],

                    // $sort: Immediately re-sorts the array by timestamp (-1 = Descending).
                    // This ensures the NEWEST song is always at index 0.
                    $sort : { "timestamp" : -1 },

                    // $slice: This is the "Cap". It keeps only the first 5 items
                    // and deletes the rest. This prevents the user document
                    // from growing infinitely large.
                    $slice: 5
                }
            }
        }
    );
}
```