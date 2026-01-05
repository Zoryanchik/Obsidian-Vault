![[Pasted image 20260105195709.png]]---

### 1. The Foundation: The "Workload First" Mindset

In SQL (Relational) databases, you design data to avoid duplication (Normalization). In NoSQL (Document) databases like MongoDB, you design data to **match your application's queries**.

Before writing a single line of code, you must identify the **Workload**:

- **What are we storing?** Users, Songs, Albums, Plays.
    
- **What are the constraints?** A document cannot be larger than 16MB. Updates are atomic only at the _single document_ level.
    
- **What is the priority?** "Logging a play" happens millions of times (Write-Heavy). "Viewing a User Profile" happens thousands of times (Read-Heavy).

![[Pasted image 20260105195839.png]]
![[Pasted image 20260105195848.png]]
![[Pasted image 20260105195856.png]]
![[Pasted image 20260105195906.png]]
### 2. The Core Decision: Embed vs. Reference

The fundamental choice in document modelling is how to connect data.

- **Embed:** Store related data inside the same document (e.g., inside an array or subdocument).
    
    - _Pros:_ Fast reads (one disk seek). Atomic updates.
        
    - _Cons:_ Document size limit (16MB). Data duplication.
        
- **Reference:** Store data in separate documents and link them via `_id`.
    
    - _Pros:_ Smaller documents. Avoids duplication.
        
    - _Cons:_ Requires multiple queries (slower) to fetch connected data .
        

**The Rule of Thumb:** "What is used together is stored together".


### 3. Modelling Relationships (By Cardinality)

The lecture breaks down how to model specific relationships based on "Cardinality" (how many items are on the other side).

#### A. One-to-One: Song & Lyrics

- **Scenario:** A song has one set of lyrics. Lyrics belong to one song.
    
- **Strategy:** **Embed**.
    
- **Why:** Lyrics don't exist without the song, and you almost always want to display them together.
    
- **Code Implementation:**
    
    JavaScript
    
    ```
    db.songs.updateOne(
      {"title": "The King of Rock 'N' Roll"},
      {$set : {"lyrics" : { "text" : "La la la...", "writer": "Paddy McAloon"}}}
    )
    ```
    
    You use `$set` to add the lyrics subdocument directly into the song document .
![[Pasted image 20260105221453.png]]![[Pasted image 20260105221502.png]] B. One-to-Few: User & Playlists

- **Scenario:** A user creates playlists. A user typically has a small number (e.g., <100), not millions.
    
- **Strategy:** **Embed**.
    
- **Why:** Playlists exist in the context of a user. We can fetch the user profile and their playlists in a single query.
    
- **Code Implementation:**
    
    JavaScript
    
    ```
    db.users.updateOne(
      {"email" : "j.doe@email.com"},
      {$push : {"playlists": {"name": "My playlist", "created": new Date()}}}
    )
    ```
    
    You use `$push` to add a playlist subdocument to the `playlists` array inside the User document .

![[Pasted image 20260105221624.png]]![[Pasted image 20260105221631.png]]![[Pasted image 20260105221641.png]]![[Pasted image 20260105221647.png]]![[Pasted image 20260105221654.png]]![[Pasted image 20260105221841.png]]![[Pasted image 20260105221931.png]]#### C. One-to-Many: Album & Songs

- **Scenario:** An album contains tracks (e.g., 10–20). Songs are "stand-alone" entities (you search for songs independently of albums).
    
- **Strategy:** **Reference (with Denormalization)**.
    
- **Why:** If we embed full songs, the Album document gets huge. If we simply reference IDs (`track_ids`), we have to run two queries to show the tracklist (one for album, one for song titles).
    
- **The Optimization (Denormalization):** We store the **Song ID** inside the Album, but we _also copy_ the **Title** and **Duration**.
    
    - _Trade-off:_ Reads are fast (1 query). Updates are slower (if a title changes, update it in two places).
        
- **Code Implementation:** We retrieve the song details and update the album's `tracks` array with simplified song objects (ID + Title + Duration) .


**Denormalization** is the deliberate decision to break that rule. You intentionally **duplicate** data across multiple documents.


Let's look at the specific example from your slides .

#### 1. The Normalized Approach (Slow)

You keep the Song details _only_ in the `Songs` collection. The `Album` document only holds a list of IDs.

**The Album Document:**

JSON

```
{
  "_id": "album_1",
  "title": "Unknown Pleasures",
  "tracks": ["song_id_1", "song_id_2"]
}
```

**The Application Logic (The Problem):** To display the album page, your app has to:

1. Query the `albums` collection to get the ID list.
    
2. Run a _second_ query against the `songs` collection to find the titles for `song_id_1` and `song_id_2`.
    

- **Result:** Two network round-trips. Slow.
    

#### 2. The Denormalized Approach (Fast)

You decide to **duplicate** the Song Title and Duration inside the Album document. You leave the rest of the song data (like lyrics, producer, detailed stats) in the `Songs` collection.

**The Album Document:**

JSON

```
{
  "_id": "album_1",
  "title": "Unknown Pleasures",
  "tracks": [
    {
      "id": "song_id_1",
      "title": "Disorder",      // DUPLICATED DATA
      "duration": "3:29"      // DUPLICATED DATA
    },
    {
      "id": "song_id_2",
      "title": "Day of the Lords", // DUPLICATED DATA
      "duration": "4:47"           // DUPLICATED DATA
    }
  ]
}
```

**The Application Logic (The Solution):** To display the album page, your app queries the `albums` collection **once**. It immediately has the titles and durations needed to render the screen.

- **Result:** One network round-trip. Fast.
    

---

### Implementation Code (How to "Copy-Paste")

You have to write code to handle this duplication. When you add songs to an album, you fetch their details and stamp them into the album document.

JavaScript

```
// 1. You have a list of new song IDs for the album
let track_ids = [ObjectId('...'), ObjectId('...')];

// 2. Fetch the specific fields you want to duplicate (Title & Duration)
// We do NOT fetch the lyrics or other heavy data.
let tracks_denormalized = db.songs.find(
    { "_id": { $in: track_ids } },
    { "title": 1, "duration": 1 } 
).toArray();

// 3. Write this duplicated data permanently into the Album document
db.albums.updateOne(
    { "title": "Unknown Pleasures" },
    { $set: { "tracks": tracks_denormalized } }
);
```

![[Pasted image 20260105222416.png]]**Step 1: Fetch the Artist Data** We retrieve the artist's ID and Name (we don't need their bio or members list for this).

JavaScript

```
let artist_d = db.artists.findOne(
  { "name": "Joy Division" },
  { "name": 1 } // Projection: Return ONLY the ID (default) and Name
);
```

**Step 2: Stamp it onto the Album** We update the album document to include this artist object.

JavaScript

```
db.albums.updateOne(
  { "title": "Unknown Pleasures" },
  { $set: { "artist": artist_d } }
);
```

### 6. The Final Data Structure

**The Artist Document (Parent):**

JavaScript

```
{
  "_id": ObjectId("A1"),
  "name": "Joy Division",
  "formed": 1976,
  "members": ["Ian", "Peter", "Bernard", "Stephen"]
  // Notice: NO list of albums here. It stays small.
}
```

**The Album Document (Child):**

JavaScript

```
{
  "_id": ObjectId("B1"),
  "title": "Unknown Pleasures",
  "released": 1979,
  "producer": "Martin Hannett",
  // The Reference + Denormalized Name
  "artist": {
    "_id": ObjectId("A1"),
    "name": "Joy Division" 
  },
  // The Tracks (Denormalized from previous steps)
  "tracks": [ ... ] 
}
```

### Summary of Benefits

1. **Fast Reads:** The Album document now has everything needed to display the album page (Title, Tracks, Artist Name) without doing a single Join or extra query.
    
2. **Scalability:** The Artist document never gets too big, even if they release 500 albums.
    
3. **Consistency:** Since an Artist's name ("Joy Division") rarely changes, the risk of having outdated names in the Album documents is very low.

#### D. One-to-Millions: User & Plays

- **Scenario:** A user listens to songs. Over time, this history grows infinitely (unbounded).
    
- **Strategy:** **Parent Referencing (Separate Collection)**.
    
- **Why:** We cannot embed millions of plays in the User document (16MB limit). We cannot store an array of millions of IDs either.
    
- **Implementation:** We create a dedicated `Play` collection. Each play document stores a reference to the User (`user_id`).
    
    JavaScript
    
    ```
    db.plays.insertOne({
      "timestamp": new Date(),
      "user": user_id, // Reference to Parent
      "song": song_id
    })
    ```
    
![[Pasted image 20260105222710.png]]![[Pasted image 20260105222809.png]]
![[Pasted image 20260105223113.png]]![[Pasted image 20260105223056.png]]![[Pasted image 20260105223226.png]]![[Pasted image 20260105223234.png]]Put simply: **`: 1` means "Yes, please include this specific field in the result."**

![[Pasted image 20260105223655.png]]JavaScript

```
db.users.findOne(
  // PART 1: Find the User Document
  { "email": "j.doe@email.com" }, 

  // PART 2: The Projection (The Filter INSIDE the result)
  { "playlists": { $elemMatch: { "name": "My playlist" } } }
).playlists[0] 
```


![[Pasted image 20260105223845.png]]![[Pasted image 20260105223857.png]] More examples with reference
Here are three small, self-contained programs based on the concepts shown in your slides. I have referenced which image each concept comes from so you can connect the code back to your study material.

### 1. The "Clean Fetch" (Projection)

Concept: fetching only specific fields to save bandwidth.

Reference: This uses the : 1 syntax shown in the first image.

JavaScript

```java
// Scenario: We want to display a list of song titles on a webpage.
// We don't need the lyrics, duration, or producer info right now.

var myCursor = db.songs.find(
    { "artist": "Queen" },   // 1. Filter: Find songs by Queen
    { "title": 1, "_id": 0 } // 2. Project: Return ONLY the title. Hide the ID.
);

// Output result will look like:
// { "title": "Under Pressure" }
// { "title": "Bohemian Rhapsody" }
```

### 2. The "Playlist Adder" (Update with Positional Operator)

Concept: Adding an item to a specific array inside a document.

Reference: This uses the $push and $ syntax shown in the first image.

JavaScript

```java
// Scenario: Adding a new song to the "Road Trip" playlist for user "j.doe".

var newSong = { "title": "Don't Stop Believin'", "artist": "Journey" };

db.users.updateOne(
   // 1. Find the user AND the specific playlist by name
   { "email": "j.doe@email.com", "playlists.name": "Road Trip" },

   // 2. Push the new song into the 'tracks' array of THAT specific playlist
   // The '$' represents the index of the "Road Trip" playlist found in step 1.
   { 
     $push: { "playlists.$.tracks": newSong } 
   }
);
```

### 3. The "Specific Playlist Fetcher" ($elemMatch)

Concept: Retrieving only the relevant item from an array, ignoring the rest.

Reference: This uses the $elemMatch syntax shown in the second image.

JavaScript

```java
// Scenario: The user clicks "Open Gym Mix". We need to load ONLY that playlist.
// We don't want to load their other 49 playlists.

var userProfile = db.users.findOne(
    { "email": "j.doe@email.com" }, 
    { 
      // Filter the 'playlists' array to return only the element matching this name
      "playlists": { $elemMatch: { "name": "Gym Mix" } } 
    }
);

// Accessing the result
// Since it returns an array (even if it's just one item), we grab the first one (index 0).
var gymPlaylist = userProfile.playlists[0];

print("Current Playlist: " + gymPlaylist.name);
```

**Would you like me to write a small "delete" program to show how to remove a song from that playlist?**