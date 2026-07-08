  *C
  ![[Pasted image 20250210220154.png]]
  
  *  .syntax unified
.global _start 
_start:
    mov r1,#77
    mov r2, r1          @ you can also copy values between registers.
    add r1, r2          @ r1 = r1 + r2
    sub r1, r2          @ r1 = r1 - r2
    sub r1, #-33        @ r1 = r1 - 33
    @ f = (g+h) - (i+j);
    add r5, r1, r2
    add r3, r1
    sub r5, r2
    @ lets create the biggest positive and play around with overflow
    mov r1, #0x1             @ r1 = 0x1
    lsl r1, #31              @ r1 = 0x80000000 = -   -2147483648
    sub r1, #1               @ this should not cause an overflow
    adds r1, #1              @ this should cause an overflow
    @ lets play with shift now
    mov r1, #0x1             @ r1 = 0x1
    lsl r1, #31              @ Shift bits logically left
    lsr r1, #31              @ Shoft bits logically right
    lsl r1, #31              @ Shift bits logically left
    asr r1, #31              @ Shift bits arithmetically left
    @ Initialize some registers with bits
    @ to check logical operators
    mov r1, #0xffff
    mov r2, #0x1111
    @ logical not
    AND r0,r1,r2
    nop
    @ logical or
    ORR r0,r1,r2
    nop
    @ logical xor
    eor r0, r1, r2
    nop
    @ not operation
    mvn r0,r1
    nop
    @ (not r) is equivalent to r xor (0xffffffff)
    mov r0, #0xffff
    movt r0, #0xffff
    eor r1, r0
    nop
    b _start