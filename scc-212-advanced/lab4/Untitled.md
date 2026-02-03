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
![[Pasted image 20260203224441.png]]![[Pasted image 20260203224454.png]]![[Pasted image 20260203225303.png]]
haskell

```haskell
data Cmp = LESSER | EQUAL | GREATER
 deriving (Show)
```

This creates a new data type called `Cmp` with three possible values. This is safer than using numbers because you can't accidentally do math with `LESSER` or `EQUAL`!
**ensures the data type can be compared (using == ) and displayed (using show )**
## What You Need to Write

haskell

```haskell
compareOrder :: Ord a => a -> a -> Cmp
```

This function signature means:

- **`Ord a =>`**: This is a **typeclass constraint** - it means the type `a` must support ordering operations (like `<`, `>`, `==`)
- **`a -> a -> Cmp`**: Takes two values of the same type and returns a `Cmp`

## Why Do We Need the `Ord` Constraint?

The `Ord a =>` part is **required** because inside the function you need to use comparison operators:

- `x < y` (less than)
- `x == y` (equal to)
- `x > y` (greater than)

Not all types can be compared! For example:

- ✅ Numbers can be compared: `5 < 10`
- ✅ Strings can be compared: `"apple" < "banana"`
- ❌ Functions can't be compared: `(\x -> x + 1) < (\x -> x * 2)` ← This doesn't make sense!

So `Ord a =>` tells Haskell: "This function only works with types that can be ordered/compared."

## The Implementation

haskell

```haskell
compareOrder :: Ord a => a -> a -> Cmp
compareOrder x y
  | x < y     = LESSER    -- If x is less than y
  | x == y    = EQUAL     -- If x equals y
```