![[Pasted image 20250221165917.png]]
![[Pasted image 20250221170007.png]]
![[Pasted image 20250221170126.png]]
`BGE` checks if a comparison meets the **greater than or equal** condition and then branches (jumps) to a specified label if the condition is met.
![[Pasted image 20250221170256.png]]
![[Pasted image 20250221170414.png]]
![[Pasted image 20250221170830.png]]
should be str
```Assembly
.syntax unified
.data
fibs: .zero 48        @ "array" F[ ] of 12 words
str: .asciz "Hello World!"
.text
_start:
    @ load the address of the fibs array into r0	  
    ldr r0, =fibs       @ Load address of fibs array into R0
    mov r1, #0          @ First Fibonacci number (F[0] = 0)
    str r1, [r0]        @ Store at fibs[0]
    mov r1, #1          @ Second Fibonacci number (F[1] = 1)
    str r1, [r0, #4]    @ Store at fibs[1] (4 bytes ahead)
    mov r1, #2          @ Counter for loop (starting from F[2])
    add r0, #8          @ Move R0 to fibs[2] (next available word)

    @ main fibonacci loop
fib_loop:
    @ reads fibs [n-1] and fibs [n-2]
    ldr r2, [r0, #-4]  @ Load fibs[n-1] (previous value)
    ldr r3, [r0, #-8]  @ Load fibs[n-2] (two steps back)
    add r2, r3  Compute fibs[n] = fibs[n-1] + fibs[n-2]
    @ stores fibs [n] = fibs [n-1] + fibs [n-2]
    str r2, [r0] stores R2 in r0
    add r1, #1   Increases the value of `r1` by 1
    add r0, #4   @ Move to next word in memory
    @ loop condition
    cmp r1, #12  @ Process 12 characters max
    bne fib_loop  @ Repeat until 12 numbers are computed
    
    @ second program
    @ load the address of the str array into r0
    ldr r0, =str
    mov r1, #0
cap_loop:
    @ read the ASCII character
    ldrb r2, [r0, r1]
    @ check if the character is lowercase
    cmp r2, #97	  @ ASCII code for 'a'
    blt cap_skip
    cmp r2, #122  @ ASCII code for 'z'
    bgt cap_skip
    @ convert the character to uppercase and save. 
    sub r2, #97   @ ASCII code for 'a'
    add r2, #65   @ ASCII code for 'A'
    strb r2, [r0, r1]
    @ loop end condition; read only 12 characters
cap_skip:
    add r1, #1
    cmp r1, #12
    bne cap_loop
    nop 
    b _start```

