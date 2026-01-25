![[Pasted image 20260124194515.png]]![[Pasted image 20260124194752.png]]![[Pasted image 20260124194802.png]]![[Pasted image 20260124195017.png]]![[Pasted image 20260124195225.png]]![[Pasted image 20260124195354.png]]![[Pasted image 20260124195551.png]]![[Pasted image 20260124195616.png]]The provided slides explain the mechanics of **currying**, **partial application**, and **operator sections** in functional programming. These concepts allow functions to be more flexible and modular by treating multiple arguments as a sequence of single-argument functions.

---

## 1. Curried Functions

Currying is the technique of translating a function that takes multiple arguments into a sequence of functions, each with a single argument.

- **Functions Returning Functions**: A function with multiple arguments is possible by returning functions as results.
    
- **The `add'` Example**: In the function `add' x y = x + y`, the function first takes an integer `x` and returns a new function, `add' x`. This new function then takes an integer `y` to return the final result, x+y.
    
- **Multiple Arguments**: This process can be nested for any number of arguments. For instance, `mult x y z` takes `x` to return a function, which takes `y` to return another function, which finally takes `z` to return the product.
    
- **Type Signatures**: Currying is reflected in the types using arrows, such as `Int -> (Int -> Int)` for two arguments or `Int -> (Int -> (Int -> Int))` for three.
    

---

## 2. Partial Application

Curried functions are considered more flexible than functions that take tuples because they can be **partially applied**.

- **Flexibility**: Useful functions can be created by providing only some of the required arguments to a curried function.
    
- **Examples of Partial Application**:
    
    - `add' 1`: A function of type `Int -> Int` that adds 1 to its input.
        
    - `take 5`: A function of type `[Int] -> [Int]` that takes the first 5 elements of a list.
        
    - `drop 5`: A function of type `[Int] -> [Int]` that removes the first 5 elements of a list.
        

---

## 3. Operator Sections

Haskell provides a special syntax called **sections** to convert standard operators (like `+`) into curried functions or partially applied functions using parentheses.

- **Infix to Prefix**: An operator written _between_ two arguments (infix) can be converted into a curried function written _before_ its arguments (prefix) by wrapping it in parentheses, such as `(+) 1 2`.
    
- **Defining Sections**: You can include one of the arguments inside the parentheses to create a partially applied function.
    
    - `(1+)`: A function that adds 1 to its argument.
        
    - `(+2)`: A function that adds 2 to its argument.
        
- **General Rule**: If ⊕ is an operator, then `(⊕)`, `(x⊕)`, and `(⊕y)` are all considered **sections**.
![[Pasted image 20260124195938.png]]![[Pasted image 20260124200219.png]]![[Pasted image 20260124200233.png]]![[Pasted image 20260124200520.png]]![[Pasted image 20260124200602.png]]![[Pasted image 20260124200705.png]]![[Pasted image 20260124200809.png]]![[Pasted image 20260124200835.png]]![[Pasted image 20260124201008.png]]![[Pasted image 20260124201109.png]]![[Pasted image 20260124201249.png]]![[Pasted image 20260124201440.png]]![[Pasted image 20260125033214.png]]![[Pasted image 20260125033245.png]]![[Pasted image 20260125033330.png]]![[Pasted image 20260125033339.png]]![[Pasted image 20260125033412.png]]![[Pasted image 20260125033437.png]]
![[Pasted image 20260125033924.png]]
## 1. Partial Function (The Left Side)

A partial function is one that is not defined for all possible values of its input type.

- **The Code:** `abs n | n >= 0 = n`
    
- **The Problem:** The type signature says it takes an `Int`, but the logic only provides a result if `n` is 0 or greater.
    
- **The Result:** If you pass a negative number (e.g., -5), the program doesn't know what to do. It will likely crash or throw a "non-exhaustive patterns" error. It "partially" covers the range of integers.
    

## 2. Total Function (The Right Side)

A total function is "safe" because it is defined for every possible value of its input type.

- **The Code:** ```haskell abs n | n >= 0 = n | otherwise = -n
    
- **The Solution:** By adding the `otherwise` case (which handles all negative numbers), the function now covers the **total** range of the `Int` type.
    
- **The Result:** No matter what integer you provide, the function will always return a valid result and will not crash due to missing logic.
![[Pasted image 20260125033954.png]]![[Pasted image 20260125034002.png]]![[Pasted image 20260125034008.png]]