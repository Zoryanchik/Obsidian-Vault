blt **ransfers control to the specified target instruction if value1 is less than or equal to value2**
![[Pasted image 20250222175101.png]]
```    
.global arr_mean

   .type arr_mean, %function

arr_mean:

      ldr r0,=arr @pointer to array

      mov r1, #1

      ldr r2, [r0]  @

  @ Add code to estimate mean

  mean_loop:

  ldr r3, [r0, r1, lsl 2]

  add r2, r3

  lsr r2, 1

  add r1, #1

  cmp r1, #10

 blt mean_loop

 mov r0, r2

 bx lr