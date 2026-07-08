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

Here is the rewritten and formatted version of **Task 3**, including the instructions and the corresponding JavaScript/MongoDB shell code for each step.

### **Task 3: Modelling a New Entity**

See the Album – Song relationship. An album must contain multiple songs, and a song may belong to one album. A list of songs on an album is provided in `album_tracks.json`.

---

### **3.1. Create an Album document (Embedded)**

**Task:** Create an `Album` document (in an `albums` collection) with the fields: `Title` "Unknown Pleasures", `Released` 1979, and the list of songs (from `album_tracks.json`) embedded.

**Code:**

JavaScript

```java
// Load the JSON data (Node.js environment)
const fs = require('fs');
const r = fs.readFileSync('album_tracks.json');
const tracks = JSON.parse(r);

// Insert the album with embedded tracks
db.albums.insertOne({
    "title": "Unknown Pleasures",
    "released": 1979,
    "tracks": tracks
});
```

---

### **3.2. Print the Album Details**

**Task:** Print the album details, including the track listing (list of song details).

**Code:**

JavaScript

```java
// Find and print specific fields
db.albums.find(
    { "title": "Unknown Pleasures" },
    { 
        "_id": 0, 
        "title": 1, 
        "released": 1, 
        "tracks.title": 1,
        "tracks.duration": 1 
    }
);
```

---

### **3.3. Delete the Album**

**Task:** Delete the album created in the previous step to prepare for the referencing model.

**Code:**

JavaScript

```java
db.albums.deleteOne({ "title": "Unknown Pleasures" });
```

---

### **3.4. Add Songs to Collection (Retaining IDs)**

**Task:** Add the songs from `album_tracks.json` to the `songs` collection. Retain the `_ids` created (returned from `insertMany`) by using `Object.values()` to extract an array of ID values.

**Code:**

JavaScript

```java
// Insert tracks into the separate 'songs' collection
let added = db.songs.insertMany(tracks);

// Extract the generated _ids into an array
let track_ids = Object.values(added.insertedIds);
```

---

### **3.5. Create Album Document (Referenced)**

**Task:** Create the `Album` document again, this time including the list of album songs as **references** (using the array of IDs).

**Code:**

JavaScript

```java
db.albums.insertOne({
    "title": "Unknown Pleasures",
    "released": 1979,
    "tracks": track_ids  // Storing only the IDs
});
```

---

### **3.6. Print Album Details (Resolving References)**

**Task:** Print the album details, including the list of song titles. This involves fetching the album first, then using the stored IDs to fetch the song details.

**Code:**

JavaScript

```java
// 1. Fetch the album
let album = db.albums.findOne({ "title": "Unknown Pleasures" });

// 2. Fetch the songs using the IDs found in the album
let track_details = db.songs.find(
    { "_id": { $in: album.tracks } },
    { "title": 1, "duration": 1, "_id": 0 }
);

// 3. Print the formatted output
print(album.title + " (" + album.released + ")");

// Loop through the cursor to print track details
for (let track of track_details) {
    print(track.title + " (" + track.duration + ")");
}
```