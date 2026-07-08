![[Pasted image 20251113204228.png]]![[Pasted image 20251113204303.png]]![[Pasted image 20251113204333.png]]![[Pasted image 20251113204530.png]]![[Pasted image 20251113204555.png]]A **value** can be a string, number, object (nested), array, boolean
![[Pasted image 20251113204818.png]]![[Pasted image 20251113205739.png]]![[Pasted image 20251113205804.png]]![[Pasted image 20251113205839.png]]![[Pasted image 20251113210002.png]]The main challenge in NoSQL data modelling is balancing the application's needs, database performance, and data retrieval patterns .

The key decision is whether to use **Embedded Documents** or **Referenced Documents**.

### Embedded Documents (Denormalized Model)

- **What it is:** Storing related data together in a single document, often as a sub-document or an array.
    
- **Example:** A `user` document that contains a nested `contact` sub-document .
    
- **Pros:**
    
    - Allows applications to retrieve and manipulate related data in a **single database operation**.
        
    - Fewer queries are needed.
        
- **Cons:**
    
    - Can lead to data **duplication** and redundancy.
        

### Referenced Documents (Normalized Model)

- **What it is:** Storing related data in separate documents and collections, using **references** (like foreign keys) to link them.
    
- **Example:** A `user` document and a separate `contact` document , where the `contact` document holds a `user_id` field that references the user's `_id`.
    
- **Pros:**
    
    - More flexible and avoids data duplication.
        
    - Better for representing complex many-to-many relationships.
        
- **Cons:**
    
    - Requires **more queries** (or "roundtrips") to the server to fetch related data.![[Pasted image 20251113210356.png]]
    ![[Pasted image 20251113210427.png]]![[Pasted image 20251113210442.png]]![[Pasted image 20251113210500.png]]![[Pasted image 20251113210534.png]]