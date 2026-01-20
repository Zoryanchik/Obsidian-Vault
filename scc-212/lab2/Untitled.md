![[Pasted image 20260120171534.png]]![[Pasted image 20260120171541.png]]![[Pasted image 20260120172137.png]]![[Pasted image 20260120172313.png]]![[Pasted image 20260120172332.png]]![[Pasted image 20260120172623.png]]![[Pasted image 20260120172816.png]]![[Pasted image 20260120172857.png]]

|**Expression (Input)**|**Type Signature (Output)**|**Explanation (Why?)**|
|---|---|---|
|**Lists of Functions**|||
|`[tail, init, reverse]`|`[[a] -> [a]]`|A list of functions. Each function takes a list `[a]` and returns a new list `[a]`.|
|`[head, last]`|`[[a] -> a]`|A list of functions. Each function takes a list `[a]` and extracts a single element `a`.|
|`[length, sum]`|`Num b => [[a] -> b]`|A list of functions. Each function takes a list `[a]` and returns a number `b`.|
|`[(*2), (+1), abs]`|`Num a => [a -> a]`|A list of math functions. Each takes a number `a` and returns a number `a`.|
|`[even, odd]`|`Integral a => [a -> Bool]`|A list of predicate functions. Each takes an integer `a` and returns `True` or `False` (`Bool`).|
|`[show]`|`Show a => [a -> String]`|A list containing the `show` function, which converts `a` to a String.|
|**Complex Data Structures**|||
|`([1,2], ['a','b'])`|`Num a => ([a], [Char])`|A **tuple** (fixed size). First element is a list of numbers; second is a list of characters.|
|`[(1, 'a'), (2, 'b')]`|`Num a => [(a, Char)]`|A **list of tuples**. Every item in the list must be a pair of `(Number, Char)`.|
|`[[1,2], [3,4,5]]`|`Num a => [[a]]`|A **list of lists**. The inner lists can be different lengths, but must contain the same type (numbers).|
|`(True, "Hello", 5)`|`Num a => (Bool, [Char], a)`|A **3-tuple** (triple). It contains exactly three specific types in that order.|


|**Constraint Prefix**|**When it appears**|**Example Expression**|
|---|---|---|
|**`Num a =>`**|When using integers (`5`) or basic math (`+`, `-`, `*`).|`[1, 2, 3]`|
|**`Fractional a =>`**|When using decimals (`3.14`) or division (`/`).|`[1.5, 2.5]`|
|**`Eq a =>`**|When checking equality (`==` or `/=`).|`x == y`|
|**`Ord a =>`**|When comparing size (`<`, `>`, `min`, `max`).|`x > y`|


![[Pasted image 20260120173446.png]]![[Pasted image 20260120173942.png]]![[Pasted image 20260120173954.png]]![[Pasted image 20260120174232.png]]![[Pasted image 20260120174546.png]]XS IS A LIST
![[Pasted image 20260120180627.png]]![[Pasted image 20260120181420.png]]
**The Error:** You cannot divide a number by an integer directly in Haskell. `length xs` returns an `Int`, but the division operator (`/`) expects both sides to be generic numbers (like `Float` or `Double`). **The Fix:** You must convert the length to a number using `fromIntegral`.
### 1. `Eq` vs. `Ord`

- **`Eq` (Equality):** This only allows you to check if two things are **equal** (`==`) or **not equal** (`/=`). It has no concept of "bigger" or "smaller."
    
- **`Ord` (Ordering):** This allows you to check **order** (`>`, `<`, `>=`, `<=`).

![[Pasted image 20260120182201.png]]
