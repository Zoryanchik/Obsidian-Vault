![[Pasted image 20250228212550.png]]
![[Pasted image 20250228213651.png]]
![[Pasted image 20250228234212.png]]
The **Vector Table** is a list of **memory addresses** that store the starting addresses (**vectors**) of **interrupt service routines (ISR)** or **exception handlers**.
When an interrupt or exception happens:

- The CPU **stops current execution**.
- Goes to the vector table.
- Fetches the **address of the ISR** for that particular interrupt.
- Jumps to that address to execute the ISR.
- After ISR finishes, the CPU **resumes** the previous task.
- ![[Pasted image 20250301021802.png]]
![[Pasted image 20250301022247.png]]
![[Pasted image 20250301022512.png]]
![[Pasted image 20250301162043.png]]
![[Pasted image 20250301162212.png]]
