![[Pasted image 20260105235906.png]]

Here are the MongoDB shell statements for **Task 3: Modelling a new entity**.

This task explores the difference between **Embedding** (storing related data inside the document) and **Referencing** (storing a link to data in another collection).

### **Pre-requisite: Define the JSON data**

Since I do not have access to your `album_tracks.json` file, I have defined the variable `albumTracks` below with the real tracklist for the album _"Unknown Pleasures"_ by Joy Division. **Run this block first.**

JavaScript

```java
var albumTracks = [
    { title: "Disorder", artist: "Joy Division", released: 1979 },
    { title: "Day of the Lords", artist: "Joy Division", released: 1979 },
    { title: "Candidate", artist: "Joy Division", released: 1979 },
    { title: "Insight", artist: "Joy Division", released: 1979 },
    { title: "New Dawn Fades", artist: "Joy Division", released: 1979 },
    { title: "She's Lost Control", artist: "Joy Division", released: 1979 },
    { title: "Shadowplay", artist: "Joy Division", released: 1979 },
    { title: "Wilderness", artist: "Joy Division", released: 1979 },
    { title: "Interzone", artist: "Joy Division", released: 1979 },
    { title: "I Remember Nothing", artist: "Joy Division", released: 1979 }
];
```

---

### **3.1 Create Album with Embedded Songs**

We create a new album document and store the full list of songs directly inside it.

JavaScript

```java
db.albums.insertOne({
    Title: "Unknown Pleasures",
    Released: 1979,
    songs: albumTracks
})
```

### **3.2 Print Album Details**

We use `findOne` to verify the album and its embedded tracks are saved.

JavaScript

```java
db.albums.findOne({ Title: "Unknown Pleasures" })
```

### **3.3 Delete the Album**

We delete the document we just created to prepare for the next approach (referencing).

JavaScript

```java
db.albums.deleteOne({ Title: "Unknown Pleasures" })
```

### **3.4 Add Songs to `songs` Collection & Retain IDs**

Now we insert the tracks into the main `songs` collection instead. We capture the result in a variable (`result`) so we can access the automatically generated `_id` for each song.

JavaScript

```java
// 1. Insert the tracks into the songs collection
var result = db.songs.insertMany(albumTracks);

// 2. Extract the _ids using Object.values() as requested
var songIds = Object.values(result.insertedIds);

// Optional: Print to verify we have the IDs
printjson(songIds);
```

### **3.5 Create Album with References**

We create the album again, but this time, instead of the full song details, we only store the array of `_id`s we captured in the previous step.

JavaScript

```java
db.albums.insertOne({
    Title: "Unknown Pleasures",
    Released: 1979,
    songs: songIds
})
```

### **3.6 Print Album Details (Resolving References)**

If we just did a standard `findOne` here, we would only see a list of ID numbers (e.g., `ObjectId("...")`). To see the actual song titles, we need to "join" the data using the `$lookup` aggregation.

JavaScript

```java
db.albums.aggregate([
    // 1. Find the specific album
    { $match: { Title: "Unknown Pleasures" } },

    // 2. "Join" with the songs collection
    {
        $lookup: {
            from: "songs",          // The collection to join with
            localField: "songs",    // The field in 'albums' containing the IDs
            foreignField: "_id",    // The matching field in 'songs'
            as: "track_details"     // The name for the output array
        }
    },

    // 3. (Optional) Make the output cleaner by showing only Title, Released, and Track Titles
    {
        $project: {
            Title: 1,
            Released: 1,
            "track_details.title": 1
        }
    }
])
```

**Next Step:** Would you like me to explain how to handle **Deleting** in this referenced model (e.g., if you delete the Album, what happens to the Songs)?