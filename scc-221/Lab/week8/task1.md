![[Pasted image 20260105233706.png]]![[Pasted image 20260105233920.png]]
![[Pasted image 20260105234226.png]]
![[Pasted image 20260105234301.png]]![[Pasted image 20260105234451.png]]Here are the MongoDB shell statements to complete your CRUD (Create, Read, Update, Delete) operations.

Since I do not have your specific `songs.json` file, I have provided a sample data set in step **1.3** that includes the specific songs required to make the later queries (like "Blue Monday", "David Bowie", etc.) work correctly for testing.

### 1.1 Create/Switch Database

In MongoDB, a database is created automatically when you switch to it and insert data.

JavaScript

```java
use lab7
```

### 1.2 Create a Single Song Document

We will insert a single song. I have chosen "Bohemian Rhapsody" for this example.

JavaScript

```java
db.songs.insertOne({
    title: "Bohemian Rhapsody",
    artist: "Queen",
    released: 1975
})
```

### 1.3 Add Song Documents (from songs.json)

Assuming you have the JSON content, you would use `insertMany`. I have constructed this list to ensure all the questions below (1.4 through 1.10) yield results.

JavaScript

```java
db.songs.insertMany([
    { title: "Blue Monday", artist: "New Order", released: 1983 },
    { title: "Starman", artist: "David Bowie", released: 1972 },
    { title: "Heroes", artist: "David Bowie", released: 1977 },
    { title: "Fly Me to the Moon", artist: "Frank Sinatra", released: 1954 },
    { title: "Jailhouse Rock", artist: "Elvis Presley", released: 1957 },
    { title: "Wonderwall", artist: "Oasis", released: 1995 },
    { title: "Smells Like Teen Spirit", artist: "Nirvana", released: 1991 },
    { title: "Under Pressure", artist: "Queen & David Bowie", released: 1982 },
    { title: "Baby Shark", artist: "Pinkfong", released: 2015 }
])
```

### 1.4 Print details of "Blue Monday"

We use `find` (or `findOne`) with a query filter.

JavaScript

```java
db.songs.find({ title: "Blue Monday" })
```

### 1.5 Print Title and Year for "David Bowie"

Here we use a **projection** as the second argument. `1` includes the field, `0` excludes it. `_id` is included by default unless explicitly excluded.

JavaScript

```java
db.songs.find(
    { artist: "David Bowie" }, 
    { title: 1, released: 1, _id: 0 }
)
```

### 1.6 Print details for songs released before 1960

We use the `$lt` (less than) comparison operator.

JavaScript

```java
db.songs.find(
    { released: { $lt: 1960 } },
    { artist: 1, title: 1, released: 1 }
)
```

### 1.7 Print details for songs released in the 1990s

We need a range here: greater than or equal to (`$gte`) 1990 AND less than or equal to (`$lte`) 1999.

JavaScript

```java
db.songs.find(
    { released: { $gte: 1990, $lte: 1999 } },
    { artist: 1, title: 1 }
)
```

### 1.8 Update "Under Pressure" release year

We use `updateOne` with the `$set` operator to modify an existing field.

JavaScript

```java
db.songs.updateOne(
    { title: "Under Pressure" },
    { $set: { released: 1981 } }
)
```

### 1.9 Increment the play count

We use the `$inc` operator. If the field `play_count` does not exist, MongoDB creates it and sets it to the increment value (1).

JavaScript

```java
db.songs.updateOne(
    { title: "Bohemian Rhapsody" },
    { $inc: { play_count: 1 } }
)
```

### 1.10 Delete "Baby Shark"

We use `deleteOne` to remove the document matching the criteria.

JavaScript

```java
db.songs.deleteOne({ title: "Baby Shark", artist: "Pinkfong" })
```

---

### Quick Reference Table: Operators Used

|**Operator**|**Meaning**|**Example Usage**|
|---|---|---|
|**$set**|Sets the value of a field|`{$set: {year: 1999}}`|
|**$lt**|Less Than|`{$lt: 1960}`|
|**$gte**|Greater Than or Equal To|`{$gte: 1990}`|

Would you like me to rewrite these specifically for a **Python script** using `pymongo`?