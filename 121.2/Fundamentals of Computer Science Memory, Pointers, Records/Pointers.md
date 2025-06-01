A **pointer** in C is a variable that stores the **memory address** of another variable. Instead of holding a value directly, a pointer points to the location in memory where the value is stored
- **Declaration**
    - A pointer is declared using the `*` symbol.
    `int *ptr; // Declares a pointer to an integer`
    
- **Initialization**
    - A pointer can be initialized with the address of a variable using the address-of operator (`&`).
    
    `int x = 10;
    `int *ptr = &x; // ptr stores the address of x`
    
- **Dereferencing**
    
    - The value stored at the memory location a pointer points to can be accessed using the dereference operator (`*`).

    `printf("%d", *ptr); // Prints the value of x (10)`

![[Pasted image 20241123222246.png]]