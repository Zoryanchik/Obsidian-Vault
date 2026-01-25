![[Pasted image 20260120024128.png]]![[Pasted image 20260120024242.png]]
Haskell

```
oddNumbers :: Int -> [Int]
oddNumbers limit = [1, 3..limit]
```

- **`oddNumbers :: Int -> [Int]`**: This is the **Type Signature**. It tells us that the function named `oddNumbers` takes a single integer (`Int`) as input and returns a list of integers (`[Int]`).
    
- **`[1, 3..limit]`**: This is Haskell's **Range Syntax**.
    
    - It starts the list at **1**.
        
    - The second number is **3**. Haskell calculates the difference between the first and second number (3 - 1 = 2) to determine the "step."
        
    - Therefore, it generates a sequence adding 2 at every step: 1, 3, 5, 7, etc.
        
    - It stops when the number exceeds the `limit`.
        
![[Pasted image 20260120024509.png]]![[Pasted image 20260120024617.png]]![[Pasted image 20260120024827.png]]![[Pasted image 20260120024844.png]]