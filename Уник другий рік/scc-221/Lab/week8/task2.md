![[Pasted image 20260105234940.png]]![[Pasted image 20260105234947.png]]![[Pasted image 20260105234957.png]]Here are the MongoDB shell statements for Task 2.

**Note:** To ensure the commands below work (since these specific songs weren't in the previous `songs.json` example), please run this **Setup Block** first to add the necessary songs to your database:

JavaScript

```Java
db.songs.insertMany([
    { title: "Blackbird", artist: "The Beatles", released: 1968 },
    { title: "Time After Time", artist: "Cyndi Lauper", released: 1983 },
    { title: "Louie Louie", artist: "Richard Berry", released: 1957 },
    { title: "Louie Louie", artist: "The Kingsmen", released: 1963 },
    { title: "Louie Louie", artist: "The Beach Boys", released: 1964 },
    { title: "Respect", artist: "Otis Redding", released: 1965 },
    { title: "Respect", artist: "Aretha Franklin", released: 1967 },
    { title: "Burning Down the House", artist: "Talking Heads", released: 1983 },
    { title: "Burning Down the House", artist: "Tom Jones and The Cardigans", released: 1999 },
    { title: "Burning Down the House", artist: "Paramore", released: 2024 }
]);
```

---

### 2.1 Embedding Documents

In this approach, we store the data of the cover song directly inside the parent song's document. This is good for read performance if you always want to see the covers when viewing the original song.

**Statement for "Blackbird" (Beyoncé cover):**

JavaScript

```Java
db.songs.updateOne(
    { title: "Blackbird", artist: "The Beatles" },
    {
        $push: {
            covers: {
                title: "BLACKBIIRD",
                artist: "Beyoncé",
                released: 2024
            }
        }
    }
);
```

**Statement for "Time After Time" (Mabel cover):**

JavaScript

```java
db.songs.updateOne(
    { title: "Time After Time", artist: "Cyndi Lauper" },
    {
        $push: {
            covers: {
                title: "Time After Time",
                artist: "Mabel",
                released: 2021
            }
        }
    }
);
```
let cover_song = {
    "title": "Time After Time", 
    "artist": "Mabel",
    "released": 2021
};

db.songs.updateOne( 
    { "title": "Time After Time", "artist": "Cyndi Lauper" }, 
    { 
      $push: { "covers" : cover_song } 
    } 
);
### 2.2 Referencing Documents

Here, we only store the `_id` of the cover song in the `covers` array. This keeps the original document smaller and prevents data duplication (normalization), but requires a second query (lookup) to get the details of the cover.

We use JavaScript variables in the shell to capture the `_id` first.

**1. "Louie Louie" (Richard Berry -> Kingsmen & Beach Boys):**

JavaScript

```java
// Find the covers
var kingsmen = db.songs.findOne({ title: "Louie Louie", artist: "The Kingsmen" });
var beachboys = db.songs.findOne({ title: "Louie Louie", artist: "The Beach Boys" });

// Update the original
db.songs.updateOne(
    { title: "Louie Louie", artist: "Richard Berry" },
    { 
        $push: { 
            covers: { 
                $each: [ kingsmen._id, beachboys._id ] 
            } 
        } 
    }
);
```

_(Note: `$each` allows pushing multiple items at once)_

**2. "Respect" (Otis Redding -> Aretha Franklin):**

JavaScript

```java
var aretha = db.songs.findOne({ title: "Respect", artist: "Aretha Franklin" });

db.songs.updateOne(
    { title: "Respect", artist: "Otis Redding" },
    { $push: { covers: aretha._id } }
);
```

**3. "Burning Down the House" (Talking Heads -> Tom Jones & Paramore):**

JavaScript

```java  
var tomJones = db.songs.findOne({ artist: "Tom Jones and The Cardigans" });
var paramore = db.songs.findOne({ artist: "Paramore", title: "Burning Down the House" });

db.songs.updateOne(
    { title: "Burning Down the House", artist: "Talking Heads" },
    { 
        $push: { 
            covers: { 
                $each: [ tomJones._id, paramore._id ] 
            } 
        } 
    }
);
```

### 2.3 Referencing the Other Side (Inverse)

This adds a reference on the "child" document pointing back to the "parent". This is useful if you want to find out "Is this song a cover? If so, of what?".

We will add a `cover_of` field to the **Aretha Franklin** version of "Respect", pointing back to **Otis Redding**.

JavaScript

```java
// 1. Find the parent song (Otis Redding)
var originalRespect = db.songs.findOne({ title: "Respect", artist: "Otis Redding" });

// 2. Update the child song (Aretha Franklin) to link back to the parent
db.songs.updateOne(
    { title: "Respect", artist: "Aretha Franklin" },
    { $set: { cover_of: originalRespect._id } }
);
```
same shit
```java
// 1. Find the Child song first (Aretha Franklin)
var coverVersion = db.songs.findOne({ 
    title: "Respect", 
    artist: "Aretha Franklin" 
});

// 2. Update the Parent song (Otis Redding) to add the child to a 'covers' list
db.songs.updateOne(
    { title: "Respect", artist: "Otis Redding" },
    { 
      $push: { 
        covers: coverVersion._id 
      } 
    }
);
```