![[Pasted image 20260218035458.png]]![[Pasted image 20260218035504.png]]![[Pasted image 20260218035511.png]]
## 1. The Type Signature

Haskell

```
count :: Char -> String -> Int
```

- **`Char`**: The first input is the character you are looking for (e.g., `'s'`).
    
- **`String`**: The second input is the text you are searching through (e.g., `"Mississippi"`).
    
- **`Int`**: The output is the total count of those characters found.
    

---

## 2. The Logic (The Comprehension)

The heart of the function is this line: `count x xs = length [x' | x' <- xs, x == x']`

To understand this, read it from right to left like a filter:

1. **`x' <- xs`**: (The Generator) "For every character **x'** in the string **xs**..."
    
2. **`x == x'`**: (The Guard/Filter) "...keep it **only if** it is equal to the character **x** we are looking for."
    
3. **`x'`**: (The Output) "Collect all those matching characters into a new list."
    
4. **`length [...]`**: Finally, count how many items ended up in that new list.
    

---

## 3. Walkthrough Example

If we run `count 's' "Mississippi"`, here is what happens behind the scenes:

- The comprehension looks at every letter in "Mississippi".
    
- It discards 'M', 'i', 'p', etc., because they don't match 's'.
    
- It keeps every 's' it finds.
    
- The intermediate result is a temporary list: `['s', 's', 's', 's']`.
    
- The `length` function counts those 4 elements and returns **4**.