```
    .global arr_sum
.type arr_sum, %function
arr_sum:
  @ r0 arr addr, r1 counter, r2 sum, 
  @ r3 tmp reg.
```
.type arr_sum, %function
The %function is a modifier that says that arr_sum is function, meaning its need to be executed 

```
@ r0 -> pointer to array, r1 -> counter, r2 -> sum
  ldr r0, =arr
  mov r1, #0
  mov r2, #0
```
ldr is used to create a pointer that can acces data in array
 ```
 cmp r1, #10

  @compare if r1 = 10

  blt   sum_loop

  @branch if less or equal to 10

  mov r0, r2

  bx lr
  ```
ble is branch if less or equal bx lr return our r0 value
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

arr_mean:

  @ Add code to estimate mean

  bx lr

  

    .global arr_sort

arr_sort:

  @ TODO add code to sort data

  bx lr

  

  .global _start

_start:

  

  bl arr_sum

  

  bl arr_mean 

  

  bl arr_sort

  

loop:

   nop

  b loop

