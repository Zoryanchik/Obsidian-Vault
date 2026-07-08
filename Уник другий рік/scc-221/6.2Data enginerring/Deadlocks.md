![[Pasted image 20251110231105.png]]![[Pasted image 20251110231249.png]]![[Pasted image 20251110231401.png]]### 1. The Concept: "Waits-For" Graph

A deadlock is a "circular wait" condition where two or more transactions are stuck waiting for each other to release resources (locks).

To find a deadlock, we draw a **"Waits-For" Graph**:

- The circles (`T1`, `T2`, etc.) are the transactions.
    
- We draw an arrow from `Tx` to `Ty` (**`Tx -> Ty`**) if `Tx` is forced to **wait** for `Ty` to release a lock.
    
- **A cycle in this graph means there is a deadlock.**
    

### 2. Tracing the Schedule to Build the Graph

Let's follow the schedule (left-to-right) to see who holds which locks and who is waiting.

1. **`T1: S(A), R(A)`**
    
    - T1 requests and gets a **Shared lock on A**.
        
    - **Locks Held:** `T1` holds `S(A)`.
        
2. **`T2: X(B), W(B)`**
    
    - T2 requests and gets an **Exclusive lock on B**.
        
    - **Locks Held:** `T1` holds `S(A)`, `T2` holds `X(B)`.
        
3. **`T1: S(B), R(B)`**
    
    - T1 tries to get a Shared lock on `B`.
        
    - **CONFLICT:** T2 already holds an _Exclusive_ lock on `B`. T1 cannot proceed.
        
    - **Result:** T1 must **wait** for T2.
        
    - **Graph Update:** We draw **`T1 -> T2`**.
        
4. **`T3: S(C), R(C)`**
    
    - T3 requests and gets a **Shared lock on C**.
        
    - **Locks Held:** `T1` holds `S(A)`, `T2` holds `X(B)`, `T3` holds `S(C)`.
        
    - **Waiting:** `T1` (for `T2`).
        
5. **`T2: X(C), W(C)`**
    
    - T2 tries to get an Exclusive lock on `C`.
        
    - **CONFLICT:** T3 already holds a _Shared_ lock on `C`. T2 cannot proceed.
        
    - **Result:** T2 must **wait** for T3.
        
    - **Graph Update:** We draw **`T2 -> T3`**.
        
6. **`T4: X(B), W(B)`**
    
    - T4 tries to get an Exclusive lock on `B`.
        
    - **CONFLICT:** T2 already holds an _Exclusive_ lock on `B`. T4 cannot proceed.
        
    - **Result:** T4 must **wait** for T2.
        
    - **Graph Update:** We draw **`T4 -> T2`**. (Note: This wait is real, but it's not part of the final cycle).
        
7. **`T3: X(A), W(A)`** (This is the critical step, shown in red)
    
    - T3 tries to get an Exclusive lock on `A`.
        
    - **CONFLICT:** T1 already holds a _Shared_ lock on `A`. T3 cannot proceed.
        
    - **Result:** T3 must **wait** for T1.
        
    - **Graph Update:** We draw **`T3 -> T1`**.
        

### 3. The "DEADLOCK!" Conclusion

Let's look at the "Waits-For" graph we just built. We have found a **cycle**:

- T1 is waiting for T2 (to release lock on B).
    
- T2 is waiting for T3 (to release lock on C).
    
- T3 is waiting for T1 (to release lock on A).
    

This is a circular chain **(`T1 -> T2 -> T3 -> T1`)** where no transaction can ever proceed. They are all permanently stuck waiting for each other. This is a deadlock.

(Note: The graph drawn on the slide is confusing and incomplete. The _true_ waits-for graph, derived from the schedule's logic, is what reveals the deadlock.)
![[Pasted image 20251110231714.png]]![[Pasted image 20251110232137.png]]This slide explains a **Recoverable Schedule**, which is a rule to prevent one of the worst types of database anomalies.

Here's the simple breakdown and the answer to the question.

### The Rule Explained

A schedule is **recoverable** if it avoids making "dirty reads" permanent.

The rule on the slide says: "a transaction $T$ is not allowed to **Commit** until all other transactions that wrote values that $T$ read have committed."

- **In simpler terms:** If Transaction $T_1$ reads data written by Transaction $T_2$, then $T_2$ _must_ commit _before_ $T_1$ is allowed to commit.
    
- **Why?** To prevent a situation where $T_1$ commits permanent changes based on $T_2$'s "dirty" (uncommitted) data, only for $T_2$ to abort later. That would leave the database in a corrupt, inconsistent state.
    

---

### Is (a) or (b) recoverable?

The answer is: **(b) is recoverable.**

Here is the analysis of both schedules:

#### Schedule (a): NOT Recoverable

1. **`T2: w(x)`**: $T_2$ writes a value to $x$. This is temporary, "dirty" data.
    
2. **`T1: r(x)`**: $T_1$ reads the "dirty" value of $x$ from $T_2$.
    
3. **`T1: commit`**: $T_1$ **commits**, making its work permanent.
    
4. **`T2: abort`**: $T_2$ fails and aborts. Its change to $x$ is rolled back (undone).
    

- **This is a disaster.** $T_1$ has now committed permanent changes to the database based on a value of $x$ that _never officially existed_. The database is now corrupt, and this error is **unrecoverable**. This schedule violated the rule.
    

#### Schedule (b): IS Recoverable

1. **`T2: w(x)`**: $T_2$ writes a value to $x$.
    
2. **`T1: r(x)`**: $T_1$ reads the "dirty" value of $x$ from $T_2$.
    
3. **`T2: abort`**: $T_2$ fails and aborts.
    
4. **`T1: abort`**: Because $T_1$ read data from the failed $T_2$, the system forces $T_1$ to abort as well. This is called a **cascading abort**.
The rule (that $T_1$ cannot commit before $T_2$) was never broken.
![[Pasted image 20251110232619.png]]This schedule is still **recoverable** because no transactions committed any bad data. However, it's extremely inefficient. All the work done by T1 and T2 was completely wasted, which is a problem that advanced database systems try to avoid.