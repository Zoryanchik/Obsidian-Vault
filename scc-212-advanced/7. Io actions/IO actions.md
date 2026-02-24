![[Pasted image 20260224020554.png]]![[Pasted image 20260224020939.png]]![[Pasted image 20260224021051.png]]![[Pasted image 20260224021159.png]]![[Pasted image 20260224021313.png]]
## Ответ Gemini

---

### 1. An IO Action (`act1`, `act4 y`)

These are standalone actions. When the computer reaches these lines, it simply executes the task (e.g., printing a string). Notice that `act1` doesn't save its result anywhere; it just runs.

### 2. A Generator (`x <- act2`)

This is how you "extract" a value from an action.

- `act2` might be something like `getLine` (which waits for a user to type).
    
- The `<-` arrow takes the result of that action and binds it to the name `x`.
    
- You can now use `x` in the following lines.
    

### 3. A Let Clause (`let y = fnc x`)

This is for **pure logic**. Unlike the generators above, `let` doesn't involve "actions" or the outside world. It is used to perform calculations or transform data using standard functions.

- **Key difference:** You don't use `<-` here because there is no "action" to run; you are just giving a name (`y`) to a calculation.
    

### 4. The Last Line Rule

The slide notes that the **last line must return an IO type**. In Haskell, a `do` block is actually one big single action made of smaller ones. To make the whole block valid, the very last thing it does must result in an `IO` action (like `act4 y`).

![[Pasted image 20260224021911.png]]
![[Pasted image 20260224022102.png]]
