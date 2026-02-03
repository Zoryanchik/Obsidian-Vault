![[Pasted image 20260203174934.png]]![[Pasted image 20260203174926.png]]![[Pasted image 20260203175016.png]]

``` Java
-- 1. Define the type alias
-- We tell Haskell that 'StudentName' is just another name for 'String'
type StudentName = String

-- 2. Define a function using the alias
-- Notice how the type signature reads more like a sentence:
-- "greet takes a StudentName and returns a String"
greet :: StudentName -> String
greet name = "Hello, " ++ name ++ "!"

-- 3. Testing it out
main :: IO ()
main = do
    -- You can use the alias explicitly
    let student1 :: StudentName = "Alice"
    
    -- Or just use a regular String (because they are the same thing!)
    let student2 :: String = "Bob"
    
    print (greet student1)  -- Output: "Hello, Alice!"
    print (greet student2)  -- Output: "Hello, Bob!"
```
![[Pasted image 20260203180410.png]]![[Pasted image 20260203184426.png]]![[Pasted image 20260203184437.png]]![[Pasted image 20260203184550.png]]![[Pasted image 20260203184630.png]] 