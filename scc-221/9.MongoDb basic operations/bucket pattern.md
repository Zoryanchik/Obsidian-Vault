![[Pasted image 20260105225527.png]]![[Pasted image 20260105225557.png]]**Problem:** Storing one document per play wastes space (indexes) and is slow to read. **Solution:** Group 50 plays into one "Bucket" document. **Code:**
- **Without Buckets:** You throw all 5,000 books into one giant, impossible-to-lift crate.
    
- **With Buckets:** You fill a small box with 50 books. Once it's full, you seal it and grab a fresh, empty box.

### Code Breakdown

JavaScript

```jaVA
function logPlayBucket(user_id, song_id) {
    const timestamp = new Date();

    db.plays.updateOne(
       // PART 1: The Smart Search (Finding an "Open Box")
       { "user": user_id, "count": { $lt: 50 } }, 

       // PART 2: The Action (Filling the Box)
       { 
         $push: { "plays": { "ts": timestamp, "song": song_id } },
         $inc: { "count": 1 }
       },

       // PART 3: The Safety Net (Getting a New Box)
       { "upsert": true }
    );
}
```

#### 1. The Smart Search (`$lt: 50`)

- **Code:** `{ "user": user_id, "count": { $lt: 50 } }`
    
- **Translation:** "Find me a document for this user where the `count` is **Less Than 50**."
    
- **Why?** This checks if the user has a "bucket" that is not full yet.
    

#### 2. The Update (`$push` and `$inc`)

- **`$push`**: Adds the new song play into the `plays` array of that bucket.
    
- **`$inc`**: Increments (adds 1 to) the `count` field. If the count was 49, it becomes 50. The next time you run this code, the search (step 1) will fail because 50 is not less than 50. The bucket is now "sealed."
    

#### 3. The Magic: Upsert (`upsert: true`)

This is the most critical part. It handles two scenarios automatically:

- **Scenario A (Bucket Exists):** If a bucket with space (count < 50) is found, it updates it.
    
- **Scenario B (All Buckets Full):** If _all_ existing buckets have 50 items (or if this is the user's first song ever), the search fails. **Upsert** detects this failure and immediately **creates a brand new document** (a new bucket) with a count of 1 and the new song inside.
    

### Visualizing the Data Structure

Instead of one huge array, your database will look like this:

**Bucket 1 (Full):**

JavaScript

```
{ "_id": 1, "user": "j.doe", "count": 50, "plays": [ ...50 songs... ] }
```

**Bucket 2 (Full):**

JavaScript

```
{ "_id": 2, "user": "j.doe", "count": 50, "plays": [ ...50 songs... ] }
```

**Bucket 3 (Current - being filled):**

JavaScript

```
{ "_id": 3, "user": "j.doe", "count": 12, "plays": [ ...12 songs... ] }
```

### Why use this instead of the "Subset Pattern"?

- **Subset Pattern (Previous Slide):** Good for "Last 5 songs." It deletes old data.
    
- **Bucket Pattern (This Slide):** Good for "Full History." It keeps _everything_ but organizes it efficiently so your database stays fast.