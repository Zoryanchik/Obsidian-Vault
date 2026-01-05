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