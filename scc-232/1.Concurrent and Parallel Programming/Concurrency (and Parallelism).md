![[Pasted image 20260116012249.png]]![[Pasted image 20260116012555.png]]**How this represents Concurrency:** If this is a **concurrent** system, one processor might calculate $1+6+3$ for the first array, then "pause" that task to start the second array by reading the $2$, then switch back to the first array to read the next number ($2$). Both sums are "making progress" over a period of time, even if the CPU only handles one number at a physical micro-moment.
![[Pasted image 20260116012702.png]]![[Pasted image 20260116012726.png]]![[Pasted image 20260116012954.png]]![[Pasted image 20260116013016.png]]![[Pasted image 20260116013032.png]]![[Pasted image 20260116013106.png]]![[Pasted image 20260116013328.png]]![[Pasted image 20260116013358.png]]

| **Feature**      | **Amdahl's Law**                | **Gustafson's Law**                             |
| ---------------- | ------------------------------- | ----------------------------------------------- |
| **Perspective**  | Pessimistic                     | Optimistic                                      |
| **Workload**     | **Fixed** (Same data size)      | **Variable** (Data scales with CPUs)            |
| **Focus**        | Reducing execution time         | Increasing problem size                         |
| **Scaling Type** | Strong Scaling                  | Weak Scaling                                    |
| **Bottleneck**   | The serial fraction limits you. | The serial fraction is negligible for big data. |
![[Pasted image 20260116013709.png]]![[Pasted image 20260116013720.png]]Latency is ==the time delay between an action and its response in a system==

![[Pasted image 20260116014025.png]]![[Pasted image 20260116014110.png]]![[Pasted image 20260116014305.png]]![[Pasted image 20260116014318.png]]![[Pasted image 20260116014326.png]]![[Pasted image 20260116014349.png]]![[Pasted image 20260116014454.png]]![[Pasted image 20260116014524.png]]#### 1. The Task: `void f()`

This function is the "job" that will be executed.

- **The Loop:** It counts from 0 to 4.
    
- **The Output:** It prints the current number followed by the string "steps".
    
- **The Delay:** `std::this_thread::sleep_for(...)` tells the thread to pause for 500 milliseconds. This is used here to simulate a task that takes time to complete, making it easier to see how the two threads overlap.
    

#### 2. The Execution: `int main()`

- **Thread Creation:** `std::thread t1(f);` and `std::thread t2(f);` create two independent threads. As soon as these lines run, both `t1` and `t2` start executing the function `f()` simultaneously.
    
- **Joining:** `t1.join();` and `t2.join();` are crucial. They tell the main program to "wait" until both threads have finished their work before closing the program. Without these, the program might exit while the threads are still trying to print to the screen.
    

---

### Why the output is "Strange" (Non-determinism)

The slide asks if you see anything strange with the input (it likely meant **output**). Because `t1` and `t2` are running at the same time and sharing `std::cout`, their messages will likely get jumbled.

Instead of seeing a clean list like: `0 steps, 1 steps...` followed by another `0 steps, 1 steps...`

You might see something like this:

Plaintext

```
0 steps
0 steps
1 steps
1 steps
...
```

Or even worse, the characters might interleave because `std::cout` is not "thread-safe" in this context:

Plaintext

```
0 0 stepssteps
```

### Key Takeaway

This happens because of the **OS Scheduler**. You cannot predict exactly when the computer will switch focus from Thread 1 to Thread 2. This unpredictability is called **non-determinism**. To fix this in real-world coding, you would use a **Mutex** (mutual exclusion) to ensure only one thread talks to the screen at a time.