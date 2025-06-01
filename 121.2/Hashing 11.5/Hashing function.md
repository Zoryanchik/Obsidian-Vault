**Hashing Basics**:

- Hashing transforms keys into numerical indices using a hash function to store and retrieve data efficiently.
- The hash table uses these indices to determine data storage buckets, ensuring faster operations.
- Converts a key (often a string to an integer)
- Integer is used for indexing a storage array.
- The same deterministic function is used for storing and retrieving data 
- Index integer is not just restricted to 0 to 25.
- Hence, data can be spread across a much longer array.
- Collusion can be dealt with by chaining
![[Pasted image 20250114132354.png]]![[Pasted image 20250114132605.png]]![[Pasted image 20250114132727.png]]![[Pasted image 20250114132816.png]]![[Pasted image 20250114132959.png]]![[Pasted image 20250114133112.png]]![[Pasted image 20250114133131.png]]- **Designing Effective Hash Functions**:
    
Good hash functions distribute data uniformly to minimize collisions.
    - Simple functions like summing character values demonstrate limitations in range and collision handling.
    - Advanced techniques include:
        - Using mathematical operations (multiplication and bit-shifting) for efficient computation.
        - Modulo operations to constrain indices to the table size.

![[Pasted image 20250114133429.png]]



