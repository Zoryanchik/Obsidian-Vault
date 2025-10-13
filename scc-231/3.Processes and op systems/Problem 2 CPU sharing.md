![[Pasted image 20251013213044.png]]When a process is currently running on the CPU, the operating system itself is **not running** — the CPU is executing **user code** (the process’s instructions).  
The OS can only perform a **context switch** (i.e., stop one process and start another) when **it regains control of the CPU**.
The OS is not _constantly in control_ of the CPU. Instead, control switches between:

1. **User mode** — process code executes.
    
2. **Kernel mode** — OS code executes.
    

When the process is in **user mode**, the OS can’t just interrupt it at will unless a **hardware event** occurs to transfer control back to the kernel.
#CoperativeSharing: Long-running processes periodically give up the CPU for the OS to run other tasks.   
#NonCoperative :In **preemptive** scheduling, the OS _can forcibly take back control_ of the CPU at fixed intervals (called **time quanta** or **time slices**) using a **hardware timer interrupt**.![[Pasted image 20251013213408.png]]![[Pasted image 20251013213423.png]]![[Pasted image 20251013213440.png]]