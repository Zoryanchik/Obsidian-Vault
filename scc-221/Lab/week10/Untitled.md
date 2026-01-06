Here are comprehensive study notes for Lab 9. I have organized them by task and question number, adding a clear explanation above each code snippet so you can understand the _logic_ behind the syntax.

---
![[Pasted image 20260106190046.png]]
# SCC.221 Lab 9: MongoDB Study Notes

## **Task 1: Basic Queries & Cursors**

_Focus: using `.find()`, projections, sorting, and dot notation for embedded fields._

### **1.1 Find the 20 most played songs**

**Logic:**

1. **Empty Filter `{}`**: We want to consider all songs.
    
2. **Projection**: We only need specific fields (`artist`, `title`, `total_plays`). We explicitly exclude `_id` (`"_id": 0`) to clean up the output.
    
3. **Sort**: `-1` means descending (highest plays first). We add a secondary sort on `_id` to ensure a consistent tie-break order.
    
4. **Limit**: Restricts the result to just the top 20.
    

JavaScript

```java
//
function mostPlayedSongs(topN) {
    return db.songs.find({}, 
        {"artist": 1, "title": 1, "total_plays": 1, "_id": 0})
        .sort({"total_plays": -1, "_id": 1})
        .limit(topN);
}
```

### **1.2 Top songs by a specific artist**

Logic:

This is the same as 1.1, but we add a filter {"artist": artist} inside the .find() method. This acts like a WHERE clause in SQL.

JavaScript

```java
//
function artistTopSongs(artist, topN) {
    return db.songs.find({"artist": artist},
    {"artist": 1, "title": 1, "total_plays": 1, "_id": 0})
    .sort({"total_plays": -1, "_id": 1})
    .limit(topN);
}
```

### **1.3 User plays per month (Simple Sort)**

Logic:

We filter the plays collection for a specific user and year. Since the data is already stored in "buckets" (one document per month), we just need to return the month and count fields and sort them chronologically (1-12).

JavaScript

```java
//
function userMonthlyPlays(username, year) {
    return db.plays.find(
        {"user" : username, "year": year}, 
        {"month": 1, "count": 1, "_id":0})
        .sort({"month": 1})
}
```

### **1.4 & 1.5 Finding Embedded Data ("Dot Notation")**

Logic:

The albums collection has an array called tracks.

- **Dot Notation (`"tracks.title"`)**: MongoDB allows you to query inside an array of objects directly. If _any_ track in the array matches "Today", the album is returned.
    
- **Positional Operator (`$`)**: In Question 1.5, we only want to see the _specific track_ that matched, not the whole list. Using `"tracks.$": 1` in the projection tells MongoDB: "Only return the array element that matched the query part."
    

JavaScript

```java
// 1.5: Only show the matching track
function t1q5() {
    return db.albums.find({"tracks.title": "Today"},
        {"title": 1, "artist": 1, "released": 1, "tracks.$": 1});
}
```

### **1.6 Longest Songs (Formatting output)**

Logic:

The duration is stored in a sub-document: duration: { minutes: 5, seconds: 2 }.

We sort by duration.minutes first (descending), and then duration.seconds (descending) to handle ties. The solution uses a JavaScript loop to iterate over the cursor and format the seconds (adding a leading "0" if less than 10) for a pretty print format like "8:05".

JavaScript

```java
//
function t1q6() {
    let cursor = db.songs.find( {"artist": "The Beatles"}, 
        {"title": 1, "duration": 1, "_id": 0} )
        .sort({"duration.minutes": -1, "duration.seconds": -1})
        .limit(5);

    for (let doc of cursor) {
        // Logic to add leading zero for seconds < 10
        if (doc.duration.seconds < 10) {
            doc.duration.seconds = "0" + doc.duration.seconds;
        }
        console.log(doc.title + " - " + doc.duration.minutes + ":" + doc.duration.seconds);
    }
}
```

### **1.7 Regex Pattern Matching**

Logic:

We use a Regular Expression (RegEx) to find partial text matches.

- `^`: Anchors to the start of the string.
    
- `Blue`: The text we want.
    
- `\b`: A "word boundary". This ensures we match "Blue Suede Shoes" but NOT "Blueberry Hill".
    

JavaScript

```java
//
function t1q7() {
    return db.songs.find({"title": {$regex: /^Blue\b/}}).size();
}
```

### **1.8 The `$elemMatch` Trap (Important!)**

Logic:

We need an album with a track that starts with "Red" AND is > 6 minutes long.

- **Wrong Way:** `find({"tracks.title": "Red", "tracks.duration": {$gt: 6}})`
    
    - _Why?_ This finds an album where _one_ track is named "Red" and _another_ (different) track is > 6 mins.
        
- **Right Way (`$elemMatch`)**: This forces MongoDB to check that **both** conditions are met by the **same** array element (the same specific song).
    

JavaScript

```java
//
function t1q8() {
    return db.albums.find({ "tracks": 
        { $elemMatch: {"title": {$regex: /^Red/}, "duration.minutes": {$gte: 6} } } },
        {"title": 1, "artist": 1,"tracks.$": 1});
}
```

---

## **Task 2: Aggregation Pipelines**

_Focus: Processing data in stages (`$match` -> `$group` -> `$project`)._

### **2.1 & 2.2 Statistics using `$group`**

Logic:

We group all documents together to calculate stats.

- `_id: null`: This means "don't group by any specific field; treat the whole collection as one big group."
    
- `$min`, `$max`, `$avg`: Standard math accumulators.
    
- `$size`: Counts the number of elements in the `tracks` array before calculating the min/max/avg.
    

JavaScript

```java
//
function t2q1() {
    return db.albums.aggregate( [
        { $group: { 
            "_id": null, // Group everything into one bucket
            "minYear": {$min: "$released"},
            "maxYear": {$max: "$released"},
            "meanYear": {$avg: "$released"},
            "minTracks": {$min: {$size: "$tracks"}}, // Count array size first
            "maxTracks": {$max: {$size: "$tracks"}}
        } }
    ] );
}
```

### **2.3 Top Artists (Grouping by Field)**

**Logic:**

1. **`$group`**: Instead of `null`, we group by `"$artist"`. This creates one result document per unique artist.
    
2. **`$sum`**: We add up the `total_plays` field for every song belonging to that artist.
    
3. **`$set` / `$unset`**: Cosmetic stages to rename `_id` (which contains the artist name) back to `artist` for a cleaner output.
    

JavaScript

```java
//
function topArtistsByPlays(topN) {
    return db.songs.aggregate( [
        { $group: { 
            "_id": "$artist",
            "artist_plays": {$sum: "$total_plays"}
        } },
        { $set: {"artist" : "$_id"} }, // Rename _id to artist
        { $unset: ["_id"] },           // Remove the old _id field
        { $sort: {"artist_plays": -1, "artist": 1} },
        { $limit: topN }
    ]);
}
```

### **2.5 Filtering Groups (`HAVING` clause)**

Logic:

We want artists with at least 5 albums.

1. **`$group`**: Count how many albums exist per artist (`$sum: 1`).
    
2. **`$match` (after group)**: This acts like a SQL `HAVING` clause. It filters the _results_ of the grouping. We only keep docs where `count` >= 5.
    

JavaScript

```java
//
function albumsPerArtist() {
    return db.albums.aggregate([
        {$group: {
            "_id": "$artist",
            "count": {$sum: 1},
            // ... min/max year calcs
        } },
        {$match: {"count": {$gte: 5}}}, // Filter groups here
        {$set: {"artist": "$_id"}},
        {$unset: ["_id"]},
        {$sort: {"count": -1, "artist": 1}},
    ]);
}
```
![[Pasted image 20260106191607.png]]
### **2.7 Advanced Grouping (Decades)**

Logic:

We need to group by decade (1960s, 1970s), but we only have a released year (1964).

- `$toString`: Convert 1964 to "1964".
    
- `$substrBytes`: Take the first 3 characters ("196").
    
- $concat: Add "0s" to the end -> "1960s".
    
    This derived string becomes our _id for grouping.
    

JavaScript

```java 
//
function artistAlbumsByDecade(artist) {
    return db.albums.aggregate( [
        { $match: {"artist": artist}},
        { $group: { 
            // Calculate decade string dynamically
            "_id": {$concat: [{$substrBytes: [{$toString: "$released"}, 0, 3]}, "0s"]},
            "count": {$sum: 1},
            "albums": {$push: {"title": "$title", "year": "$released"}}
        } },
        { $sort: {"_id": 1}}
    ]);
}
```

---

## **Task 2.8+: The `$unwind` Operator**

_Focus: working with the `plays` collection._

The Concept:

The plays collection uses "Bucketing". One document represents one user's plays for a whole month. Inside that document is an array called plays containing the actual songs.

- To count individual songs, we must break this array apart.
    
- `$unwind: "$plays"` splits the array. If a document has 50 songs in the array, `$unwind` outputs 50 documents, each with one song.
    

### **2.8 User Top Artists (`$unwind`)**

**Logic:**

1. **`$match`**: First, find only the documents for the specific user (Performance tip: do this before unwind!).
    
2. **`$unwind`**: explode the `plays` array. Now we have one document per song played.
    
3. **`$group`**: Group by `"$plays.artist"` (the artist inside the unwound array) and count them.
    

JavaScript

```
//
function userTopArtists(username, topN) {
    return db.plays.aggregate( [
        {$match: {"user": username} }, // Filter user
        {$unwind: "$plays"},           // Explode array
        {$group: {
            "_id": "$plays.artist",    // Group by artist in the array
            "count": {$sum: 1}
        } },
        {$set: {"artist" : "$_id"}},
        {$unset: ["_id"]},
        {$sort: {"count": -1, "artist": 1}},
        {$limit: topN}
    ]);
}
```

### **2.9 & 2.10 Optimization (Double Match)**

Logic:

We want to count plays for "The Beatles".

1. **First `$match`**: `{"plays.artist": artist}`. This finds bucket documents that contain _at least one_ Beatles song. This filters out irrelevant users/months immediately.
    
2. **`$unwind`**: Break the array apart.
    
3. **Second `$match`**: `{"plays.artist": artist}`. Now that the array is broken, the document might contain a Rolling Stones song (because the user listened to both that month). We must filter _again_ to keep **only** the Beatles songs.
    

JavaScript

```
//
function artistPlaysOverYear(artist, year) {
    return db.plays.aggregate( [
        {$match: {"year": year, "plays.artist": artist} }, // 1. Filter Buckets
        {$unwind: "$plays"},                               // 2. Explode
        {$match : {"plays.artist": artist}},               // 3. Filter Songs
        {$group: {
            "_id": "$month",
            "count": {$sum: 1}
        } },
        {$sort: {"month": 1}}, // implicit sort by _id is ok, but explicit is clearer
    ]);
}
```

### **2.11 Date Operators**

Logic:

The timestamp inside the array is a proper Date object. We can use $dayOfMonth inside the $group stage to extract just the day number (1-31) for daily statistics.

JavaScript

```
//
function userPlaysOverMonth(username, year, month) {
    return db.plays.aggregate( [
        {$match: {"user": username, "year": year, "month": month} },
        {$unwind: "$plays"},
        {$group: {
            "_id": {$dayOfMonth: "$plays.timestamp"}, // Extract Day
            "count": {$sum: 1}
        } },
        {$sort: {"_id": 1}}
    ] )
}
```