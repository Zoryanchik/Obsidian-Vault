![[Pasted image 20251016135052.png]]
![[Pasted image 20251016135258.png]]
![[Pasted image 20251016140327.png]]
![[Pasted image 20251016140343.png]]![[Pasted image 20251016140356.png]]
1. What happens if you send a `SIGTERM` signal to the modified infinite loop program using the `kill` command? Does it exit gracefully or does it terminate immediately? Why?
    
    > The process will terminate immediately when it receives the `SIGTERM` signal, since this the default behavior of the signal.
    > Kill -15 7304
    > Kill SIGTERM
    
2. What happens if you try to handle a signal that is not supported by the OS? For example, you can try to handle the `SIGKILL` signal, which cannot be caught or ignored. How does the program behave in this case?
    
    > SIGKILL is one of the signal that you cannot redefine the behavior. Registerring a handler will fail with an exception.
    
3. A good way to terminate a program is to use the exit system call (_i.e._, `sys.exit(0)`). What is the significance of the argument `0` (You can read about it in the [python documentation](https://docs.python.org/3/library/sys.html#sys.exit)) or by using the help pages in Linux `man 3 kill`)? What happens if you pass a non-zero value to `sys.exit()`? You can experiment by changing the argument to a non-zero value. In you terminal you can check the exit status of the last executed command using `echo $?`. What does the exit status indicate?
    
    > The argument of the exit command is the return value from a process. The command `echo $?` returns the exit status of the last executed command. An exit status of `0` typically indicates that the program completed successfully without any errors. Non-zero values indicate that an error occurred during the execution of the program. Different non-zero values can represent different types of errors, depending on how the program is designed to use them. Usually automated bash scripts use the exit status to determine if a command was successful or if it failed, and they can terminate execution.
    
    ![[Pasted image 20251016141803.png]]
    