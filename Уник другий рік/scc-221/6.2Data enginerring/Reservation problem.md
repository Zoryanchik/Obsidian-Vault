![[Pasted image 20251110215805.png]]![[Pasted image 20251110215814.png]]![[Pasted image 20251110215833.png]]![[Pasted image 20251110215903.png]]![[Pasted image 20251110215924.png]]When you label an operation or a set of operations as "atomic," it means it must be treated as a single, all-or-nothing unit.

- It **either completes 100% successfully**,
    
- ...or it **fails completely**, leaving the system in the exact state it was in before the operation began.
![[Pasted image 20251110220100.png]]![[Pasted image 20251110220306.png]]- **You (the programmer)** promise that your transaction's logic is valid (e.g., "I won't magically create money"). This is **Transaction Consistency**.
    
- **The Database (the system)** promises to handle failures (**Atomicity**) and concurrent access (**Isolation**).
![[Pasted image 20251110220535.png]]n simple terms, **isolation guarantees that transactions don't interfere with each other** while they are running at the same time.
Each transaction feels like it has the _entire database to itself_, even when thousands of other transactions are running concurrently.

![[Pasted image 20251110220718.png]]