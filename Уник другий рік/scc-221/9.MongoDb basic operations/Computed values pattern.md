![[Pasted image 20260105230120.png]]#### 3. The Computed Values Pattern

**Problem:** Calculating "Total Plays" requires counting millions of documents. **Solution:** Pre-calculate the count on the Song document. **Code:**

JavaScript

```
db.songs.updateOne(
  {"_id" : song_id}, 
  {$inc: {"total_plays": 1}}
)
```

**Explanation:** Every time a song is played, we increment this counter. Reading the "Top Tracks" chart becomes an instant lookup rather than a slow calculation .
![[Pasted image 20260105230215.png]]