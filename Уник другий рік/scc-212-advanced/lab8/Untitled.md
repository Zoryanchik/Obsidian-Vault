![[Pasted image 20260309011550.png]]![[Pasted image 20260309011634.png]]

```
runLengths :: [Int] -> [Int]
-- Base case: a single element always has a run length of 1
runLengths [_] = [1]
runLengths (x:y:rest)
  -- If the next value is bigger, we're still in an increasing run
  -- so add 1 to whatever run length y starts, then continue
  | y > x     = let (r:rs) = runLengths (y:rest) in (r+1) : r : rs
  -- Otherwise the run is broken, x gets length 1 and we start fresh from y
  | otherwise = 1 : runLengths (y:rest)
  
```