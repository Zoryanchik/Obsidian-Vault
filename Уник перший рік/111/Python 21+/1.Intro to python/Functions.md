![[Pasted image 20250415191713.png]]1. First call `do_something()`:
    
    - Uses default parameter `times=1`
        
    - Prints "Hello" once
        
    - Output: `Hello`
        
2. Second call `do_something[16]`:
    
    - This is actually a syntax error - it should be `do_something(16)` with parentheses
        
    - With the current bracket syntax, Python will try to treat `do_something` as a list/array and access index 16