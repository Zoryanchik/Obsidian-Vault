  ![[Pasted image 20250301162413.png]]- Memory addresses are assigned to hardware **registers**.
![[Pasted image 20250301162735.png]]
![[Pasted image 20250301162930.png]]
![[Pasted image 20250301162949.png]]
![[Pasted image 20250301163120.png]]
Memory Mapped I/O is a technique where **Input/Output (I/O) devices** like sensors, LEDs, or storage devices are controlled using **memory addresses** just like normal data in RAM.
nstead of using special instructions for I/O, the **CPU interacts with hardware** by simply reading and writing data to specific memory locations.
![[Pasted image 20250306152906.png]]
![[Pasted image 20250306152925.png]]
![[Pasted image 20250306153132.png]]
![[Pasted image 20250306153556.png]]
![[Pasted image 20250306153853.png]]
- **Polled I/O**: The CPU continuously checks (polls) a device's status to see if it needs attention. This can waste CPU time since the CPU is actively waiting.
    
- **Interrupt-driven I/O**: The CPU performs other tasks and waits for the device to signal (interrupt) when it needs attention. This makes better use of CPU time because the CPU only responds when necessary.![[Pasted image 20250306154311.png]]
- ![[Pasted image 20250306154706.png]]