![[Pasted image 20251016132855.png]]
## Task 1: What is a Process?

1. What is the process ID (PID) of the infinite loop program? Does the PID change each time you run the program? Why or why not?
    
    > PIDs are different for each process. They are monotonically increasing numbers assigned by the OS kernel when a new process is created. Each time you run the program, a new process is created, and thus it gets a different PID.
    
2. What happens if you run multiple instances of the infinite loop program (`python3 infinite_loop.py & python3 infinite_loop.py & python3 infinite_loop.py & python3 infinite_loop.py &`)? How can you differentiate between them using the `ps` command? Is the PID ordering in the messages sequential? Why or why not?
    
    > In this case you notice that the processes will get different PID values, which allow you to differentiate between them. The PID ordering in the messages is not sequential because the OS kernel assigns PIDs based on availability and other factors, not in a strictly sequential manner.
    
3. How accurate is the `time.sleep(1)` function in the infinite loop program? Does it guarantee that the program will print the message exactly every second? Why or why not? You can experiment by changing the sleep duration to a smaller value (e.g., `0.01` seconds) and observing the output. How does low sleep duration affect the accuracy of the timing?
    
4. > The `time.sleep(1)` function is not perfectly accurate and does not guarantee that the program will print the message exactly every second. The actual sleep duration can be affected by various factors, including system load, scheduling by the OS, and the precision of the system clock. When you change the sleep duration to a smaller value (e.g., `0.01` seconds), you may notice that the timing becomes less accurate due to the overhead of context switching and other system activities. This can lead to variations in the actual time intervals between prints. In principle an OS has a minimum time slice (quantum) that it uses to schedule processes of around 100 microseconds. Getting precise timing below this value is not possible.
    
5. Does smaller values of sleep duration lead to greater randomness in the order of the printed messages when running the command from question 2? You can experiment by changing the sleep duration to a smaller value (e.g., `0.01` seconds) and observing the output.
    
    > Yes, smaller values of sleep duration can lead to greater randomness in the order of the printed messages when running multiple instances of the program. This is because with shorter sleep durations, the processes are more likely to compete for CPU time, leading to more frequent context switches by the OS scheduler. As a result, the order in which the messages are printed can become less predictable and more interleaved, especially if the system is under load or if there are other processes running concurrently.
    
    ![[Pasted image 20251016134927.png]]![[Pasted image 20251016134936.png]]