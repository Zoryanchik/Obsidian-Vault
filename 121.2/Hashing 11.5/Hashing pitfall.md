- Hashing provides O(1) performance if collisions are rare.
- Performance drops with long chains, prompting dynamic resizing of hash tables.
- Resizing involves rehashing all elements into a larger table, ensuring continued efficiency
 ![[Pasted image 20250114133549.png]]
 ![[Pasted image 20250114133659.png]]![[Pasted image 20250114133910.png]]
 ### Key Points:

1. **Left Shift Explanation**:
    
    - A left shift operation multiplies a number by a power of 2.
    - For example, a 5-bit left shift is equivalent to multiplying the number by 25=322^5 = 3225=32. This ensures that each character contributes uniquely to the overall hash value.
2. **Encoding Process**:
    
    - Each letter in the key **"EOT"** is assigned a numeric code. For instance:
        - `'T'` → 19
        - `'O'` → 14
        - `'E'` → 4
    - These codes are represented as binary numbers for bitwise operations.
3. **Step-by-Step Hashing**:
    
    - **For 'T' (Code: 19)**:
        - Binary representation: `000000000010011`.
        - Left shift 5 places: `000001001100000` (equivalent to T×32T \times 32T×32).
    - **For 'O' (Code: 14)**:
        - Binary representation: `000000000001110`.
        - Combine `'T'` and `'O'` using a logical OR: `000001001101110` (this adds O+T×32O + T \times 32O+T×32).
        - Left shift 5 places again: `100110111000000` (equivalent to O×32+T×322O \times 32 + T \times 32^2O×32+T×322).
    - **For 'E' (Code: 4)**:
        - Binary representation: `000000000000100`.
        - Combine `'E'` with the result of the previous step using a logical OR: `100110111001100` (equivalent to E+O×32+T×322E + O \times 32 + T \times 32^2E+O×32+T×322).
4. **Final Result**:
    
    - The final hash value is `100110111001100` (in binary), which combines all three letters into a single unique value.
 