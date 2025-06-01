![[Pasted image 20241123224157.png]]
- This does the following:
        - `sizeof(Student)` calculates the memory needed to store one `Student` record.
        - `malloc(sizeof(Student))` allocates that amount of memory from the heap.
        - The pointer `pt` stores the base address of the allocated memory block.
    - You can now use `pt` to access or manipulate the `Student` record in memory.
- ![[Pasted image 20241130153734.png]]
- 