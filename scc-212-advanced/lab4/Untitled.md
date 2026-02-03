![[Pasted image 20260203223422.png]]
```java
-- The type signature exactly as requested in the worksheet

maybeDefault :: a -> Maybe a -> a

  

-- Pattern 1: If the Maybe value is (Just x), return x

maybeDefault _ (Just x) = x

  

-- Pattern 2: If the Maybe value is Nothing, return the default value

maybeDefault def Nothing = def

  
  

--maybeDefault :: a -> Maybe a -> a

--maybeDefault defaultVal (Just x) = x           -- If there's a value, return it

--maybeDefault defaultVal Nothing  = defaultVal   -- If Nothing, return default
```


![[Pasted image 20260203224342.png]]
![[Pasted image 20260203224441.png]]![[Pasted image 20260203224454.png]]