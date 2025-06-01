![[Pasted image 20250414163041.png]]![[Pasted image 20250414163232.png]]![[Pasted image 20250414163509.png]]![[Pasted image 20250414163919.png]]
![[Pasted image 20250414164117.png]]
This is a **ternary operator**:

- If `a == 0`, return `0`.
    
- Else, return `b + multiply(a - 1, b)`.
    

This is basically saying:

- Multiply `a` and `b` by adding `b` to itself `a` times.
    
- Each recursive call reduces `a` by 1, until `a` reaches 0.

##### `?`

- Part of the ternary (or conditional) operator.
    
- It's like an inline **if-else**.

condition ? value_if_true : value_if_false;



