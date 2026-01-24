![[Pasted image 20260124192348.png]]![[Pasted image 20260124192746.png]]![[Pasted image 20260124192842.png]]![[Pasted image 20260124192936.png]]- **The Function Definition**: `mult x y z = x*y*z`.
    
- **The Type Signature**: `mult :: Int -> (Int -> (Int -> Int))`.
    
- **The Step-by-Step Process**:
    
    - **First**: `mult` takes an integer `x` and returns a new function, `mult x`.
        
    - **Second**: The function `mult x` takes an integer `y` and returns another function, `mult x y`.
        
    - **Third**: Finally, the function `mult x y` takes an integer `z` and returns the final result of the calculation: $x \times y \times z$.
![[Pasted image 20260124193948.png]]

|**Partial Application Example**|**Resulting Type**|**Purpose**|
|---|---|---|
|`add' 1`|`Int -> Int`|A function that increments any number by 1.|
|`take 5`|`[Int] -> [Int]`|A function that always takes the first 5 elements of a list.|
|`drop 5`|`[Int] -> [Int]`|A function that always removes the first 5 elements of a list.|
![[Pasted image 20260124194231.png]]![[Pasted image 20260124194345.png]]