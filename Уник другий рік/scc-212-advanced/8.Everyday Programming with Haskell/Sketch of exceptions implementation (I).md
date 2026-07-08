![[Pasted image 20260305021514.png]]![[Pasted image 20260305021535.png]]![[Pasted image 20260305021618.png]]### 3. Generalizing to "IO" and "World"

The text connects this "exception" pattern to how Haskell handles the outside world (**IO**):

- **The State of the World:** Just like the exception example used a tuple to pass a "success flag," IO functions use a tuple to pass the "State of the World".
    
- **The Formula:** `type IO a = World -> (a, World)`. This means an IO action takes the current state of the universe, performs an action, and returns the result plus the _new_ state of the universe.