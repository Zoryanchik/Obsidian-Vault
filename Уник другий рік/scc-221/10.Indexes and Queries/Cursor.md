A **cursor** is a pointer to the result set of a query that allows traversal over documents. It fetches documents in batches to optimize memory and network usage.

- **Lifecycle:** Cursors remain active until all items are seen, they are manually closed, or they time out (default 10 mins).
    
- **Iteration Methods:**
    
    - `while (cursor.hasNext()) { ... }`
        
    - `cursor.forEach(printjson)`
        
    - `for (let doc of cursor) { ... }`.
        
- **Useful Cursor Functions:**
    
    - `count()`: Returns number of docs.
        
    - `limit(n)`: Restricts results to `n` documents.
        
    - `skip(n)`: Skips the first `n` documents.
        
    - `sort({field: 1})`: Sorts results (1 for ascending, -1 for descending).
        
    - `toArray()`: Converts cursor results into a single array in memory.
        
- **Chaining:** Functions can be chained. Order of `sort`, `skip`, and `limit` generally does not matter to the output (MongoDB processes them logically: sort -> skip -> limit).
![[Pasted image 20260106004035.png]]

1. **While Loop:** Uses `hasNext()` to check for more documents and `next()` to retrieve them.
    
    JavaScript
    
    ```
    while (cursor.hasNext()) { let doc = cursor.next(); printjson(doc); }
    ```
    
2. **forEach:** Applies a function to every document.
    
    JavaScript
    
    ```
    cursor.forEach(printjson)
    ```
    
3. **For...of Loop:** Iterates directly over the cursor.
    
    JavaScript
    
    ```
    for (let doc of cursor) { printjson(doc); }
    ```
    

**Important Cursor Functions:**

- `limit(n)`: Restricts the result set to `n` documents.
    
- `skip(n)`: Skips the first `n` documents.
    
- `sort({field: 1})`: Sorts results (1 for ascending, -1 for descending).
    
- `toArray()`: Iterates the cursor and appends all results to an array in memory. This allows the results to be edited or used in subsequent operations.
    
- **Chaining:** You can chain these functions. The order of sort, skip, and limit in the chain does not matter; MongoDB will always Sort -> Skip -> Limit.
![[Pasted image 20260106004333.png]]![[Pasted image 20260106004453.png]]The slide provides this example:

> `db.songs.find().sort({"released": 1})`

**What this does:**

1. Goes into the `songs` collection.
    
2. Finds all documents (`find()`).
    
3. Sorts them based on the `"released"` field in **ascending** order (meaning the oldest songs will appear first).

![[Pasted image 20260106004616.png]]![[Pasted image 20260106004642.png]]
![[Pasted image 20260106004730.png]]
![[Pasted image 20260106004813.png]]
![[Pasted image 20260106004942.png]]

| **Query**          | **Meaning**           | **Result**                             |
| ------------------ | --------------------- | -------------------------------------- |
| `{"ratings": 1}`   | Include the **field** | Returns the **full list**: `[5, 8, 9]` |
| `{"ratings.$": 1}` | Include the **match** | Returns the **single item**: `[8]`     |
- **Original Array:** `[ "A", "B", "C" ]`
    
- **Query:** `{$slice: -2}` (Get the last 2 items)
    
- **Result:** `[ "B", "C" ]`
    
    - _Notice "B" is still before "C". The order is preserved._
        

### 2. What the slide example did

In your slide, the example was `{$slice: -1}`.

- This didn't reverse anything; it just said "Give me the **last 1** item."
    
- If the ratings were `[5, 8, 9]`, it just grabbed `[9]`.