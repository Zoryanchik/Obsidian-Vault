![[Pasted image 20260203174934.png]]![[Pasted image 20260203174926.png]]![[Pasted image 20260203175016.png]]
Great question! Let me explain `type` and `newtype` in Haskell, which are related to defining types but work differently from `data`.

## `type` - Type Synonyms

`type` creates an **alias** for an existing type. It's just a different name, not a new type.

haskell

```haskell
type Name = String
type Age = Int
type Person = (Name, Age)

let john :: Person
john = ("John", 25)

-- But this is also valid:
let name :: Name
name = "Alice"

let alsoName :: String
alsoName = name  -- Works fine! Name and String are identical
```

**Key point:** `type` doesn't create type safety. The compiler treats `Name` and `String` as exactly the same thing.

haskell

```haskell
type UserId = Int
type ProductId = Int

let user = 42 :: UserId
let product = 100 :: ProductId

-- Oops! No type error:
user == product  -- Compiles fine, compares 42 == 100
```

**Use case:** Documentation and readability, not type safety.

## `newtype` - Wrapper Types

`newtype` creates a **distinct type** with exactly one constructor and one field. It provides type safety with zero runtime overhead.

haskell

```haskell
newtype UserId = UserId Int
newtype ProductId = ProductId Int

let user = UserId 42
let product = ProductId 100

-- Type error!
user == product  -- Won't compile! Different types
```

You must unwrap to get the value:

haskell

```haskell
newtype Age = Age Int
  deriving (Show)

let myAge = Age 25

-- To use the Int inside:
case myAge of
  Age n -> n + 1  -- 26
```

**Deriving with newtype:**

haskell

```haskell
newtype Email = Email String
  deriving (Show, Eq)

let addr1 = Email "john@example.com"
let addr2 = Email "john@example.com"

addr1 == addr2        -- True (derived Eq)
show addr1            -- "Email \"john@example.com\""
```


![[Pasted image 20260203180410.png]]![[Pasted image 20260203184426.png]]![[Pasted image 20260203184437.png]]![[Pasted image 20260203184550.png]]![[Pasted image 20260203184630.png]] ![[Pasted image 20260203185549.png]]![[Pasted image 20260203185612.png]]

## The Problem (Slide I)

When you create a new type in Haskell, the REPL doesn't know how to display it:

haskell

```haskell
data Person = Person String Int

-- If you try this in GHCi:
let john = Person "John" 25
john  -- Error! No instance for (Show Person)
```

The REPL can't print `john` because there's no `Show` instance telling Haskell how to convert a `Person` to a `String`.

**Manual solution** - implement `Show` yourself:

haskell

```haskell
data Person = Person String Int

instance Show Person where
  show (Person name age) = "Person " ++ name ++ " (age " ++ show age ++ ")"

-- Now this works:
let john = Person "John" 25
john  -- prints: Person John (age 25)
```

But this is tedious boilerplate!

## The Solution (Slide II)

The `deriving` keyword automatically generates typeclass instances:

haskell

```haskell
data Person = Person String Int
  deriving (Show)

let john = Person "John" 25
john  -- prints: Person "John" 25
```

Haskell automatically generated the `Show` instance by showing the constructor name and its values.

**More examples:**

haskell

```haskell
data Color = Red | Green | Blue
  deriving (Show, Eq, Ord)

Red == Green        -- False (from Eq)
Red < Blue          -- True (from Ord, based on definition order)
show Red            -- "Red" (from Show)
```

haskell

```haskell
data Temperature = Celsius Float | Fahrenheit Float
  deriving (Show, Eq)

Celsius 20.0 == Celsius 20.0     -- True
show (Fahrenheit 68.0)            -- "Fahrenheit 68.0"
```

**When NOT to use it:**

If you want custom behavior, write the instance manually:

haskell

```haskell
data Temperature = Celsius Float

-- Custom Show instance
instance Show Temperature where
  show (Celsius c) = show c ++ "°C"

Celsius 25.0  -- prints: 25.0°C
```