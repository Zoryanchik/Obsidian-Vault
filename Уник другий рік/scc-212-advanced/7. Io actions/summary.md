![[Pasted image 20260224030105.png]]
**The core idea** is that Haskell strictly separates pure code (no effects) from impure code (real world interactions). IO actions represent functions that depend on or change the state of the world.

**IO types** come in two flavours — `IO a` where you get something back (like `IO [Int]`, returns a list of ints), and `IO ()` where you're just doing something with no meaningful return value (like printing).

**`do` blocks** are how you actually chain and run IO actions. Every line in a `do` block must be an IO action of the same IO type. If you need multiple actions inside an `if` or `case`, you need a **nested `do` block** to bundle them into one single expression.

**`pure`** is how you wrap a plain value into an IO context when needed — it doesn't do any real world effect, it just "lifts" the value up so the types match. Use `pure` rather than `return` in modern Haskell.

**You cannot printf debug** because printing is an IO effect, and pure functions are contractually forbidden from having effects — their type signature would be lying if they could.

**`main`** is the entry point of every Haskell program, typed `IO ()`, and it's where all your IO actions ultimately get run from.

The big takeaway: **keep your logic in pure functions and push IO to the edges of your program.**