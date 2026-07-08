![[Pasted image 20250221215643.png]]
![[Pasted image 20250221220139.png]]
![[Pasted image 20250221220742.png]]
![[Pasted image 20250221220929.png]]
![[Pasted image 20250221221002.png]]
![[Pasted image 20250221222750.png]]
![[Pasted image 20250221223018.png]]
![[Pasted image 20250221223053.png]]
mov r0, #5    @ Load g = 5 into r0
mov r1, #6    @ Load h = 6 into r1
mov r2, #4    @ Load i = 4 into r2
mov r3, #3    @ Load j = 3 into r3
bl leaf       @ Call leaf function
**`mov pc, lr`**

- `PC = LR` (return to the caller).
- Execution jumps back to the instruction after `bl leaf`.
-