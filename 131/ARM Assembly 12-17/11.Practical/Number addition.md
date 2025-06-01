![[Pasted image 20250313155959.png]]
![[Pasted image 20250313160203.png]]
![[Pasted image 20250313160317.png]]
divide by 2 to get mean
![[Pasted image 20250313160347.png]]

![[Pasted image 20250313160542.png]]
Hacker
![[Pasted image 20250313161006.png]]
![[Pasted image 20250313161211.png]]
![[Pasted image 20250313161438.png]]

This is an ARM assembly program that performs a left shift operation iteratively. Let's break it down step by step:
LOOP:
cmp r0, #1   ; Compare R0 with 1
ble DONE     ; If R0 <= 1, branch to DONE
lsl r1, r1, #1 ; Logical shift left (R1 = R1 * 2)
sub r0, r0, #1 ; Decrement R0 by 1
b LOOP       ; Branch back to LOOP

![[Pasted image 20250313162117.png]]
cmp r0, #1   ; Compare R0 with 1
ble DONE     ; If R0 <= 1, branch to DONE
