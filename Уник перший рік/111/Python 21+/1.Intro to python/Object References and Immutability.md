![[Pasted image 20250415192551.png]]1. `x` refers to the immutable integer `10`
    
2. When passed to `change_me()`, the parameter `x` gets a copy of the reference
    
3. `x = x + 1` creates a new integer `11` and rebinds the local `x` reference
    
4. The original `x` outside the function remains unchanged1.

5. `x` refers to a mutable list `[10]`
    
6. The function receives a copy of the reference (both point to the same list)
    
7. `append()` modifies the shared list object