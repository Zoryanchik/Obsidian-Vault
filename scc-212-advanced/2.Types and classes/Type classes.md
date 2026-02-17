![[Pasted image 20260120153005.png]]![[Pasted image 20260120153046.png]]![[Pasted image 20260120153106.png]]
### 1. The Restrictive Version (Without `Num`)

Haskell

```
add :: Int -> Int -> Int
add x y = x+y
```

This version is highly restrictive. It works perfectly, but **only for whole numbers of the `Int` type**. If you try to pass `Float`s (decimals), `Double`s, or `Integer`s (arbitrary-precision whole numbers) into this function, the compiler will throw an error. You would have to write a separate `addFloat`, `addDouble`, etc., which is bad practice.

---

### 2. The Flexible Version (Using `Num`)

Haskell

```
add :: Num a => a -> a -> a
add x y = x+y
```

This is where `Num` comes in. Here is why we use it:

- **To accept _any_ numeric type:** The letter `a` is a type variable. It means "any type." However, we can't just use `a -> a -> a` without a constraint. If we tried, Haskell would complain: _"How do I know the type you pass in actually knows how to use the `+` operator? What if someone tries to add two strings or two booleans?"_
    
- **To guarantee the `+` operator works:** The `Num a =>` part is a **type class constraint**. It tells the compiler: _"Type `a` can be anything you want, **provided** it is a member of the `Num` type class."_
    
- **Connecting to Slide 1:** If you look at the first slide, it shows that any type belonging to the `Num` class is guaranteed to support the `(+)` method. Therefore, by restricting `a` to `Num`, the compiler is completely satisfied that `x + y` is a valid operation, whether `x` and `y` are `Int`s, `Float`s, or any other number type.
- ![[Pasted image 20260120153427.png]]![[Pasted image 20260120153737.png]]
```
module OverloadedExamples where

-- ==========================================
-- 1. THE OVERLOADED FUNCTION (+)
-- ==========================================
-- The type signature is: (+) :: Num a => a -> a -> a
-- This means: "I can add any two things, AS LONG AS they are Numeric."

-- Example A: Using it as Integers (a = Int)
addInts :: Int
addInts = 1 + 2  -- Result: 3

-- Example B: Using it as Floats (a = Float)
addFloats :: Float
addFloats = 1.0 + 2.0  -- Result: 3.0


-- ==========================================
-- 2. WHY IT IS "SAFER" THAN PURE POLYMORPHISM
-- ==========================================
-- Pure polymorphism (like 'length') accepts ANYTHING.
-- Overloaded functions check the type before running.

-- Example C: The Error
-- If you uncomment the line below, the code will not compile.
-- addChars = 'a' + 'b'

-- WHY IT FAILS:
-- The compiler looks at 'a' (Char).
-- It checks if 'Char' is a member of the 'Num' class.
-- It is not. So it rejects the code.
```

![[Pasted image 20260120153941.png]]

![[Pasted image 20260120154810.png]]

![[Pasted image 20260120155208.png]]![[Pasted image 20260120155517.png]]![[Pasted image 20260120155653.png]]![[Pasted image 20260120160002.png]]![[Pasted image 20260120160247.png]]![[Pasted image 20260120160258.png]]![[Pasted image 20260120160313.png]]![[Pasted image 20260120160322.png]]![[Pasted image 20260120160455.png]]![[Pasted image 20260120160515.png]]![[Pasted image 20260120160546.png]]