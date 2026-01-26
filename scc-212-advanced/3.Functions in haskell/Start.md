![[Pasted image 20260124191710.png]]![[Pasted image 20260124191801.png]]
`second :: [a] -> a`

Because `a` is just a type variable, we can use any valid name for it (for example b, c, d, or num). Note that variable names MUST start with a lowercase letter so `num` is a valid variable name. This means we could also write the type as:

`second :: [num] -> num`

which corresponds to option A.

Be careful not to confuse this with the `Num` class, which starts with a capital letter.

That said, it's good practice to stick to the convention of using simple variable names for types like a, b, c, and so on.

For reference, the quiz was:

What is the type of the following function?

`second xs = head (tail xs)`

A. `second :: [num] -> num`  
B. `second :: a -> a`  
C. `second :: [a] -> [a]`  
D. `second :: a -> [a]`  
E. None of the above

I hope this clarifies the situation. Please let me know if anything remains unclear.

Abdessalam![[Pasted image 20260124191932.png]]![[Pasted image 20260124191951.png]]