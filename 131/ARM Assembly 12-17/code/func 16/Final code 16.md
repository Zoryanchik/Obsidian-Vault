![[Pasted image 20250223171628.png]]
```
.syntax unified

  

.data

  arr: .word 100, 20, 50, 40, 30, 80, 70, 60, 90, 10

  

    .text

    .global arr_sum

   .type arr_sum, %function

arr_sum:

  @ Add code to compute sum

    @ r0 -> pointer to array, r1 -> counter, r2 -> sum

  ldr r0,=arr

  mov r1, #0

  mov r2, #0

sum_loop:

  @ Load next element in r3 (addr: r0 + r1 * 4)

  ldr r3, [r0, r1, lsl 2] @same as multiply by 4

  @r0 is address of array

  @r1 is index

  @lsl 2: This is a left shift operation (r1, lsl 2) which effectively multiplies r1 by 4. This is necessary because each array element is assumed to be 4 bytes (a 32-bit integer). So, this instruction calculates the correct memory address for arr[r1] and loads it into r3.

  @the index refers to the position of the current element in the array as the program processes it during the loop.

  add r2, r2, r3 @ Add element to our sum

  add r1, #1 @ Add add to conter

  cmp r1, #10

  @compare if r1 = 10

  blt   sum_loop

  @branch if less or equal to 10

  mov r0, r2

  bx lr

  

  

    .global arr_mean

   .type arr_mean, %function

arr_mean:

      ldr r0,=arr @pointer to array

      mov r1, #1

      ldr r2, [r0]

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

  

   .global arr_sort

.type arr_sort, %function

arr_sort:

  @ r0 arr addr, r1 swapped, r2 counter

  @ r3 tmp

  ldr r0, =arr

  add r0, #4

  mov r1, #0

  mov r2, #1

  

sort_loop:

  @ Load previous element in r3 (*(r0 - 4))

  ldr r3, [r0, -4]

  

  

  @ Load current element in r3 (*r0)

  ldr r4, [r0]

  

  @ If r3 > r4, swap elements

  cmp r3, r4

  ble skip_swap

  str r3, [r0]

  str r4, [r0, -4]

  @ record that at least one swap was made

  mov r1, #1

  

skip_swap:

  

  @ Increment counter

  add r2, #1

  @ Increment pointer to point to next element

  add r0, #4

  

  @ Exit loop if counter < 10

  cmp r2, #10

  blt sort_loop

  

  @ If no swap was made, array is sorted complete function

  cmp r1, #0

  beq sort_finish 

  

  @ Otherwise, reset loop

  ldr r0, =arr

  add r0, 4

  mov r1, #0

  mov r2, #1

  b sort_loop

  

sort_finish:

  bx lr    

  

  .global _start

_start:

  

@ bl arr_sum

  

@ bl arr_mean 

  

  bl arr_sort

  

loop:

   nop

  b loop