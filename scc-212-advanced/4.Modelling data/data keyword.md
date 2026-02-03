![[Pasted image 20260203213407.png]]![[Pasted image 20260203213521.png]]The essence of the above statement is that you use the keyword `data`, supply an optional context, give the type name and a variable number of [type variables](https://wiki.haskell.org/index.php?title=Type_variable&action=edit&redlink=1 "Type variable (page does not exist)").
![[Pasted image 20260203213848.png]]![[Pasted image 20260203214023.png]]![[Pasted image 20260203214138.png]]![[Pasted image 20260203214606.png]]![[Pasted image 20260203214622.png]]## The Type Definition (Not Shown But Implied)

First, there's a `Shape` type defined somewhere like this:

haskell

```haskell
data Shape = Circle Float Float Float  -- x, y, radius
           | Rect Float Float Float Float  -- x, y, width, height
```

## Example 1: Pattern Matching to Extract Values

haskell

```haskell
area :: Shape -> Float
area (Circle x y r) = 2 * (fromIntegral r) * pi
area (Rect x y w h) = fromIntegral (w * h)
```

**What's happening:**

1. **Function signature:** `area :: Shape -> Float` means "area takes a Shape and returns a Float"
2. **Pattern matching on Circle:**

haskell

```haskell
   area (Circle x y r) = 2 * (fromIntegral r) * pi
```

- `(Circle x y r)` - matches a Circle constructor and extracts its three values
- `x` gets the x-coordinate
- `y` gets the y-coordinate
- `r` gets the radius
- Then calculates: `2 * r * pi` (circumference formula)

3. **Pattern matching on Rect:**

haskell

```haskell
   area (Rect x y w h) = fromIntegral (w * h)
```

- `(Rect x y w h)` - matches a Rect constructor and extracts its four values
- `x`, `y` are position
- `w` is width, `h` is height
- Calculates: `w * h` (area of rectangle)

**Usage example:**

haskell

```haskell
let c = Circle 0 0 5
area c  -- Returns: 31.4159... (2 * 5 * pi)

let r = Rect 0 0 10 20
area r  -- Returns: 200.0 (10 * 20)
```

## Example 2: Pattern Matching Without Decomposing

haskell

```haskell
addToList :: Shape -> [Shape] -> [Shape]
addToList x xs = x:xs
```

**What's happening:**

- `x` is the whole Shape (not decomposed into parts)
- `xs` is a list of Shapes
- `x:xs` adds x to the front of the list
- We don't care what kind of shape it is or what values it contains

**Usage example:**

haskell

```haskell
let shapes = []
let shapes2 = addToList (Circle 0 0 5) shapes
-- shapes2 = [Circle 0.0 0.0 5.0]

let shapes3 = addToList (Rect 0 0 10 20) shapes2
-- shapes3 = [Rect 0.0 0.0 10.0 20.0, Circle 0.0 0.0 5.0]
```

## Example 3: Using Wildcards `_`

The slide mentions you can use `_` for values you don't need:

haskell

```haskell
-- If you only care about the radius, not x and y:
getRadius :: Shape -> Maybe Float
getRadius (Circle _ _ r) = Just r  -- Ignore x and y with _
getRadius (Rect _ _ _ _) = Nothing  -- Not a circle, ignore all values

-- Usage:
getRadius (Circle 10 20 5)  -- Just 5.0
getRadius (Rect 0 0 10 20)  -- Nothing
```

The `_` means "I know there's a value here but I don't need it, so don't give it a name."

## Complete Working Example

haskell

```haskell
data Shape = Circle Float Float Float 
           | Rect Float Float Float Float
  deriving (Show)

-- Extract and use specific values
area :: Shape -> Float
area (Circle x y r) = 2 * r * pi
area (Rect x y w h) = w * h

-- Don't decompose, just use the whole thing
addToList :: Shape -> [Shape] -> [Shape]
addToList x xs = x:xs

-- Use wildcards for values we don't need
getRadius :: Shape -> Maybe Float
getRadius (Circle _ _ r) = Just r
getRadius (Rect _ _ _ _) = Nothing

-- Testing:
let c = Circle 0 0 5
let r = Rect 0 0 10 20

area c           -- 31.4159...
area r           -- 200.0
getRadius c      -- Just 5.0
getRadius r      -- Nothing

let shapes = addToList c [r]
-- [Circle 0.0 0.0 5.0, Rect 0.0 0.0 10.0 20.0]
```

Does this make more sense now?
![[Pasted image 20260203215100.png]]![[Pasted image 20260203215153.png]]## . Parameterised data types (aka generics)

This line is the key example:

`data Foo a = MkFoo Int a String`

Here:

- `a` is a **type variable**
    
- `Foo a` is **not a concrete type yet**
    
- It becomes a real type only when `a` is replaced with something like `Bool`, `Int`, etc.
![[Pasted image 20260203215705.png]]![[Pasted image 20260203215742.png]]![[Pasted image 20260203220212.png]]![[Pasted image 20260203220232.png]]![[Pasted image 20260203220417.png]]![[Pasted image 20260203220530.png]]![[Pasted image 20260203220638.png]]