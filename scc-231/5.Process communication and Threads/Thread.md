![[Pasted image 20251027183239.png]]- **What is a Thread?** A thread is a separate "point of execution" within a process. You can have multiple threads running "in parallel" inside one process.
    
- **Processes vs. Threads:**
    
    - **Process:** Has its own isolated address space. Heavyweight.
        
    - **Thread:** A "lightweight" process. It shares its address space with all other threads in the _same_ process.
        
- **What Threads Share vs. What They Don't:**
    
    - **SHARED:** Address space (e.g., heap memory , global variables ), and open files.
        
    - **NOT SHARED (Private):** Each thread gets its own program counter , its own registers, and its own **stack**. (A separate stack is necessary for each thread to have its own local variables and function call history).
        
- **The Problem: Race Conditions**
    
    - Because all threads access the same data, we get race conditions.
        
    - A **critical section** is a piece of code that accesses shared data.
        
    - The code `counter += 1` on page 23 is a perfect example. It looks like one instruction, but it's really three: (1) read `counter`, (2) add 1 to the value, (3) write the new value back.
        
    - A race condition happens because the thread scheduler can swap threads at any time, leading to uncontrolled interleaving. One thread might read the value (e.g., 0), but _before it can write 1_, it gets paused. Another thread runs, reads 0, writes 1, and finishes. Then the first thread wakes up and _also_ writes 1. Both threads ran, but the counter is only 1 instead of 2.
![[Pasted image 20251027183548.png]]Separate stacks
![[Pasted image 20251027183735.png]]![[Pasted image 20251027183848.png]]![[Pasted image 20251027184059.png]]![[Pasted image 20251027184114.png]]![[Pasted image 20251027184137.png]]### A. Locks (Mutual Exclusion)

- **What it is:** A lock is an object that only one thread can "hold" at a time.
    
- **How it works:**
    
    1. Before entering a critical section, a thread tries to acquire the lock.
        
    2. If the lock is free, the thread "acquires" it and enters the critical section.
        
    3. If the lock is held by _another_ thread, the current thread **blocks** (sleeps) until the lock is released.
        
    4. When the thread leaves the critical section, it "releases" the lock, allowing another waiting thread to proceed.
        
- The Python example on page 25 uses a `threading.Lock()` to protect `counter += 1`, ensuring the final count is correct.
    

### B. Condition Variables (Coordination)

- **What it is:** Locks are for protecting data, but condition variables are for **signaling** and **coordination**. They let threads wait for a specific _condition_ to become true.
    
- **Use Case (Producer/Consumer):** Imagine one thread (Producer) adding items to a shared queue and another (Consumer) removing them.
    
    - **Problem:** What if the Consumer tries to read from an _empty_ queue? It shouldn't just spin in a loop; it should sleep until the Producer adds something.
        
- **How it works:**
    
    - `cond.wait()`: The Consumer acquires the lock, sees the queue is empty, and then calls `wait()`. This atomically (1) **releases the lock** and (2) puts the Consumer thread to sleep.
        
    - `cond.notify()`: The Producer acquires the lock, adds an item to the queue, and then calls `notify()`. This **wakes up one** sleeping Consumer thread.
        
    - The woken Consumer thread then tries to **reacquire the lock**. Once it gets the lock, it can safely check the queue and consume the new item.
        

### A Note on Python: The GIL

- Python has a **Global Interpreter Lock (GIL)**.
    
- This lock prevents _true_ parallel execution of Python code. Only **one thread can execute Python bytecode at a time**.
    
- This means Python threads **will not speed up CPU-bound code**.
    
- **HOWEVER,** race conditions _still happen_ because the OS can (and does) swap threads _between_ bytecode instructions (e.g., in the middle of `counter += 1`). So, you _still_ need locks and condition variables for correctness.



**What it is:** Locks are for protecting data, but condition variables are for **signaling** and **coordination**. They let threads wait for a specific _condition_ to become true.
![[Pasted image 20251027184540.png]]