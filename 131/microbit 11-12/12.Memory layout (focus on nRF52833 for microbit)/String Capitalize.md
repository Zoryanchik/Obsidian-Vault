![[Pasted image 20250221173617.png]]
- This checks whether `str[i]` is **not** a lowercase letter (`a-z`).
- `'a'` has an ASCII value of `97` and `'z'` has an ASCII value of `122`.
- If `str[i]` is **less than** `'a'` (`97`) or **greater than** `'z'` (`122`), it means it is **not** a lowercase letter.
- The `continue;` statement skips the rest of the loop for that iteration, meaning **it does not convert spaces, punctuation, or uppercase letters**.
#### **Understanding ASCII Manipulation:**

- Each character has an **ASCII value**.
- `'a'` is `97` and `'A'` is `65`.
- `'b'` is `98` and `'B'` is `66`, and so on.
- The difference between **uppercase and lowercase** letters is **32** (`'a' - 'A' = 97 - 65 = 32`).

#### **Mathematical Conversion:**

For any lowercase letter `ch`:

- `'a'` → `'A'`: `97 - 97 + 65 = 65 ('A')`
- `'b'` → `'B'`: `98 - 97 + 65 = 66 ('B')`
- `'c'` → `'C'`: `99 - 97 + 65 = 67 ('C')`
- and so on...
![[Pasted image 20250221174014.png]]
`LDRB` stands for **"Load Register Byte"**. It is used to load a **single byte** from memory into a register.
- `LDRB` → **Load Register Byte** (loads a single byte from memory).
- `r2` → Destination register where the loaded byte will be stored.
- `[r0, r1]` → **Memory address formed by adding `r0 + r1`**.
`BLT` (Branch if Less Than)
BGT if bigger
Branch if Not Equal