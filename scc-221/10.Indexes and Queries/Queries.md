![[Pasted image 20260105232014.png]]![[Pasted image 20260105232059.png]]![[Pasted image 20260105232110.png]]
- **Goal:** Find songs by specific bands.
    
- **Explanation:** Instead of writing multiple "OR" statements, `$in` allows you to provide a list (array). If the artist matches **any** of the names in that list, the document is returned.
- - **Condition A:** `{ "covers": { $exists: 1 } }` - The song document has a field named "covers" (regardless of its value).
    
- **Condition B:** `{ "plays": { $gt: 0 } }` - The song has been played more than 0 times.
- 
- ![[Pasted image 20260105232415.png]]![[Pasted image 20260105232631.png]]![[Pasted image 20260105232743.png]]**Code:** `db.products.find( {"ratings": {$elemMatch: {$gt: 5, $lt: 9}}} )`

- **Logic:** "Is there **at least one single element** that meets ALL these criteria at once?"
![[Pasted image 20260105233142.png]]JavaScript

```
db.users.find(
  { "playlists.name": "My playlist" }, // 1. The Search
  { "playlists.$": 1 }                 // 2. The Projection
)
```

- **What it means:** "Find the user who has a playlist named 'My playlist', and return **only that specific playlist**."