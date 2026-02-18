![[Pasted image 20260218034927.png]]![[Pasted image 20260218034940.png]]![[Pasted image 20260218034953.png]]
## 👉 `foldr` — _fold from the right_

### Conceptually:

`foldr f z [x1,x2,x3] = f x1 (f x2 (f x3 z))`

So it associates to the **right**.

### Key properties

✅ Works with **infinite lists** (sometimes!)  
✅ Good for building lists / lazy structures  
✅ Matches how lists are naturally constructed  
⚠ Can build deep recursion for strict operations

### Example

`foldr (+) 0 [1,2,3] -- 1 + (2 + (3 + 0)) = 6`

---

## 👈 `foldl` — _fold from the left_

### Conceptually:

``foldl f z [x1,x2,x3] = ((z `f` x1) `f` x2) `f` x3``

So it associates to the **left**.

### Key properties

❌ Does NOT work on infinite lists  
⚠ In lazy Haskell, builds large “thunks” (can cause space leaks)  
✅ Feels more natural if you think imperatively

### Example

`foldl (+) 0 [1,2,3] -- ((0 + 1) + 2) + 3 = 6`

---

## ⚠ Important: `foldl` vs `foldl'`

Because `foldl` is lazy in the accumulator, this:

`foldl (+) 0 bigList`

can consume lots of memory.

In real code, you usually want **strict** left fold:

`foldl' (+) 0 bigList`

(`foldl'` lives in `Data.List` and forces the accumulator at each step.)
![[Pasted image 20260218035011.png]]![[Pasted image 20260218035018.png]]![[Pasted image 20260218035031.png]]