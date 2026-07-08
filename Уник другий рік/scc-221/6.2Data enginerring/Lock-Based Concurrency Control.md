![[Pasted image 20251110223643.png]]This slide explains **Lock-Based Concurrency Control**, which is the database's primary solution to prevent all the "anomalies" (like dirty reads and lost updates) we just discussed.

Think of it as a set of traffic rules for accessing data. A **lock** is a "hall pass" that a transaction must get before it's allowed to touch a piece of data.

There are two kinds of "hall passes":

### 1. The S (Shared) Lock

- **Rule:** A transaction **must** get a **Shared lock** _before_ it can **Read** an object.
    
- **Analogy:** This is like a _reading pass_ for a library book. Multiple people (transactions) can get a "reading pass" for the same book at the same time, because just reading doesn't interfere with other readers.
    

### 2. The X (Exclusive) Lock

- **Rule:** A transaction **must** get an **Exclusive lock** _before_ it can **Write** (modify or delete) an object.
    
- **Analogy:** This is like an _editing pass_ for the library book.
    
    - Only **one person** (transaction) can get an "editing pass" at a time.
        
    - While one person has the "editing pass" (an X lock), **no one else** can get _any_ pass for that book—not even a "reading pass" (an S lock).
        
    - This guarantees that no one can read or write the data while it's in a half-finished, "dirty" state.
        

### The Example on the Slide
The slide shows the "play-by-play" of a transaction (T1) following these rules:

1. **`S(A)`**: T1 says, "I need to read A." The database gives it a **Shared lock** on A.
    
2. **`R(A)`**: Now that it has the lock, T1 is allowed to **Read** A.
    
3. **`Release_S(A)`**: T1 says, "I'm done reading A," and releases the lock, so others can access it.
    
4. **`X(B)`**: T1 says, "I need to write to B." The database gives it an **Exclusive lock** on B. (If any other transaction has a lock on B, T1 must wait in line).
    
5. **`W(B)`**: Now that it has exclusive access, T1 is allowed to **Write** to B.
    
6. **`Release_X(B)`**: T1 says, "I'm done writing to B," and releases the lock.
    

This system of "get the right lock first" is what prevents concurrent transactions from crashing into each other and corrupting the data.
![[Pasted image 20251110224417.png]]![[Pasted image 20251110224558.png]]![[Pasted image 20251110224652.png]]![[Pasted image 20251110224755.png]]Because the order of _all conflicting operations_ is identical in both schedules, **Schedule 1 is "conflict equivalent" to Schedule 2.**

Therefore, according to the definition, **Schedule 1 is a conflict serializable schedule.** This means the database can safely run this fast, interleaved schedule because it is _guaranteed_ to produce the exact same result as the simple, slow serial schedule (`T1 -> T2`).
![[Pasted image 20251110225137.png]]This slide gives an example of a "bad" interleaved schedule—one that is **not conflict serializable**.

This means this schedule is dangerous and could produce an incorrect result (an anomaly) that would not happen if the transactions were run one after another.

There are only two possible "safe" or "serial" outcomes for the database:

1. **Serial1 (T1 $\rightarrow$ T2):** T1 does _all_ its work, then T2 does _all_ its work.
    
    - The "chain of command" for _every_ piece of data is: **T1 is first, T2 is second.**
        
2. **Serial2 (T2 $\rightarrow$ T1):** T2 does _all_ its work, then T1 does _all_ its work.
    
    - The "chain of command" for _every_ piece of data is: **T2 is first, T1 is second.**
        

---

### The "Bad" Interleaved Schedule

Now let's look at the "chain of command" in the "bad" interleaved schedule:

- **For data item A:** T1 writes to it first, then T2 uses it.
    
    - The chain of command is: **T1 $\rightarrow$ T2**
        
- **For data item B:** T2 writes to it first, then T1 uses it.
    
    - The chain of command is: **T2 $\rightarrow$ T1**
        

### The Conclusion (The Problem)

The "bad" schedule is trying to be **both** `T1 -> T2` (for item A) and `T2 -> T1` (for item B) at the same time.
![[Pasted image 20251110225930.png]]![[Pasted image 20251110225945.png]]In a few words, **conflict serializable** means a concurrent (interleaved) schedule is **provably "safe."**

It's a guarantee that even though transactions are mixed up, the final result is **identical** to what it would be if the transactions had run one-by-one (serially).