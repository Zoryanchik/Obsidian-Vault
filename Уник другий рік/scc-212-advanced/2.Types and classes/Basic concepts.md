![[Pasted image 20260120143807.png]]![[Pasted image 20260120143828.png]]![[Pasted image 20260120143846.png]]![[Pasted image 20260120144520.png]]![[Pasted image 20260120144600.png]]![[Pasted image 20260120144814.png]]![[Pasted image 20260120145137.png]]![[Pasted image 20260120145224.png]]![[Pasted image 20260120145256.png]]![[Pasted image 20260120145346.png]]![[Pasted image 20260120145407.png]]![[Pasted image 20260120145418.png]]![[Pasted image 20260120145805.png]]![[Pasted image 20260120150446.png]]![[Pasted image 20260120150532.png]]![[Pasted image 20260120150538.png]]![[Pasted image 20260120150858.png]]![[Pasted image 20260120150920.png]]![[Pasted image 20260120150930.png]]![[Pasted image 20260120151033.png]]- **Arity 2:** A tuple with 2 things, like `(True, False)`. (Also called a "pair").
    
- **Arity 3:** A tuple with 3 things, like `(1, 'a', True)`. (Also called a "triple").
    
- **Arity $n$:** A tuple with $n$ things.
![[Pasted image 20260120151220.png]]![[Pasted image 20260120151240.png]]![[Pasted image 20260120151427.png]]![[Pasted image 20260120151534.png]]![[Pasted image 20260120151702.png]]![[Pasted image 20260120151731.png]]![[Pasted image 20260120151756.png]]![[Pasted image 20260120151855.png]]![[Pasted image 20260120152021.png]]![[Pasted image 20260120152211.png]]![[Pasted image 20260120152447.png]]
```
-- Take the first 3 numbers
take 3 [1, 2, 3, 4, 5]
-- Result: [1, 2, 3]

-- Take the first 2 characters from a string
take 2 "Hello"
-- Result: "He"

-- Take 0 items (returns an empty list)
take 0 [True, False]
-- Result: []

-- Zip a list of numbers with a list of characters
zip [1, 2, 3] ['a', 'b', 'c']
-- Result: [(1,'a'), (2,'b'), (3,'c')]

-- What if lengths don't match? It stops at the shorter one!
zip [1, 2, 3, 4, 5] "Hi"
-- Result: [(1,'H'), (2,'i')]

-- It returns whatever you give it
id 5
-- Result: 5

id "Hello"
-- Result: "Hello"
```