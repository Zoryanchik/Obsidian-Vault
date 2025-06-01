![[Pasted image 20250219210240.png]]
- The program declares three integer variables:
    - `a = 1`
    - `b = 2`
    - `c = a + b` (sum of `a` and `b`)

#### **2. Bytecode (Right)**
0: iconst_1   // Push constant 1 onto the stack
1: istore_1   // Store top of stack into variable 1 (a)
2: iconst_2   // Push constant 2 onto the stack
3: istore_2   // Store top of stack into variable 2 (b)
4: iload_1    // Load variable 1 (a) onto the stack
5: iload_2    // Load variable 2 (b) onto the stack
6: iadd       // Add top two stack values (a + b)
7: istore_3   // Store result into variable 3 (c)
8: return     // Return from the method

First we put in stack then store, the we put in stack 1 and 2 and then store