![[Pasted image 20260120153005.png]]![[Pasted image 20260120153046.png]]![[Pasted image 20260120153106.png]]![[Pasted image 20260120153427.png]]![[Pasted image 20260120153737.png]]
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