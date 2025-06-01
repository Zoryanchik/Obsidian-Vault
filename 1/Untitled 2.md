*
chechk
, cmp ldr arr 4 
ldr regisater arr

cmp r1,r2 r1-r2 if cmp is not met skip
BLE (Branch if Less Than or Equal
bl brunch and link bl saves pc to lr

The stack pointer (sp) points to the top of the stack. (down)(contents of register lr) or if empty previous stack content less by 12 bits

In ARM architecture, **exceptions** are special events that interrupt the normal flow of a program.
1. Synchronous Exceptions (CPU-generated)
These occur as a direct result of the execution of an instruction. 
Asynchronous Exceptions (External Events)
These occur independently of the currently executing instruction, usually triggered by external hardware:

Preserved					Nonpreserved
Saved registers: r4-r11			Temporary register: r12
Stack pointer: SP(r13)			Argument registers:r0-r3
Return address:LR(r14)			Current program status
Stack above the stack pointer 		Stack below the stack pointer

Push {r4, r5, lr} push register onto stack if push pop no touch r4,r5 are registers

Inline assembly is used to insert assembly instructions within a high-level language.

R2 to hold 2^29 +40 mov r2, #40 movt r2, #0x1000

Current Program Status Register (CPSR) - Overview
The CPSR is an ARM register that holds the processor's current state.
Its value changes with arithmetic instructions, reflecting the result of operations.
I bit - "IRQ flag": Disables IRQ interrupts (normal interrupts).
F bit - "FIQ flag": Disables FIQ interrupts (fast interrupts).
T bit - "Thumb flag": Disables Thumb mode (switches between ARM and Thumb instruction sets).
Mode: Indicates the current execution mode of the processor.
31   30   29   28      ...      7   6   5   4 - 0  
 N    Z    C    V       -       I   F   T   Mode  

10000 user 10010 irq 100011 superisor  111111 system


int a = 100, b; // 'a' is initialized with 100, 'b' is uninitialized

asm (
    "movl r0, %[a];"   // Move the value of 'a' into register r0
    "movl %[b], r0;"   // Move the value from r0 into 'b'
    
    : [b] "=r" (b)     // 'b' is an output operand stored in a register
    : [a] "r" (a)      // 'a' is an input operand stored in a register
    : "r0"             // r0 is marked as a clobbered register (meaning it will be modified)
);
clobbered register
asm volatile to avoid optimization 


#include <stdio.h>

int main() {
    int a = 1;  // Initialize 'a' to 1
    int b = 2;  // Initialize 'b' to 2
    int s;      // Declare 's' to store the sum

    // Inline Assembly to add 'a' and 'b' and store result in 's'
    __asm__ (
        "add %0, %1;"   // Assembly instruction: Add b (%1) to s (%0)
        : "=r" (s)      // Output operand: 's' stored in a register
        : "r" (a), "r" (b)  // Input operands: 'a' and 'b' stored in registers
    );

    printf("sum = %d\n", s);  // Print the result

    return 0;
}
  Interfaces: Define how hardware components communicate (examples: USB, GPIO). 
  Protocols: Set rules for data exchange between devices. 
•	Handshake Protocol: Ensures that the receiver acknowledges data sent by the sender.
•	Signals: Categorized into: 
o	Command Signals
o	Data Signals

The **Vector Table** is a list of **memory addresses** that store the starting addresses (**vectors**) of **interrupt service routines (ISR)** or **exception handlers**.
When an interrupt or exception happens:
- The CPU **stops current execution**.
- Goes to the vector table.
- Fetches the **address of the ISR** for that particular interrupt.
- Jumps to that address to execute the ISR.
- After ISR finishes, the CPU **resumes** the previous task.

; Initialize registers
mov r1, #0x1         ; Load value 0x1 into r1 - used as a bitmask for row/column selection
mov r6, #0x0         ; Clear r6 - used to build the row and column pattern

; Set Row 1
orr r6, r6, r1, lsl ROW_1  ; Activate Row 1 by shifting bitmask and OR-ing with r6

; Activate Columns 2, 3, 4, 5 for Row 1
orr r6, r6, r1, lsl COL_2  ; Set Column 2
orr r6, r6, r1, lsl COL_3  ; Set Column 3
orr r6, r6, r1, lsl COL_4  ; Set Column 4
orr r6, r6, r1, lsl COL_5  ; Set Column 5

; Write pattern to LED matrix memory address to turn on the LED
str r6, [r4]               ; Write the pattern in r6 to the address pointed by r4

; Prepare for a specific column (Column 4)
mov r6, #0x0               ; Clear r6 to isolate the bit for Column 4
orr r6, r6, r1, lsl COL_4  ; Set only Column 4
str r6, [r5]               ; Write the pattern to the address in r5 to finalize the LED state

  
; Initialize registers   2 3
mov r1, #0x1         ; Load value 0x1 into r1 - used as a bitmask for row/column selection
mov r6, #0x0         ; Clear r6 - used to build the row and column pattern

; Set Row 2
orr r6, r6, r1, lsl ROW_2  ; Activate Row 2 by shifting bitmask and OR-ing with r6

  ; Activate Columns 2, 3, 4, 5 for Row 2 (assuming similar hardware behavior)
orr r6, r6, r1, lsl COL_2  ; Set Column 2
orr r6, r6, r1, lsl COL_3  ; Set Column 3 (Target Column)
orr r6, r6, r1, lsl COL_4  ; Set Column 4
orr r6, r6, r1, lsl COL_5  ; Set Column 5

; Write pattern to LED matrix memory address to turn on the LED
str r6, [r4]               ; Write the pattern in r6 to the address pointed by r4

; Isolate Column 3 (specific to target LED if required)
mov r6, #0x0               ; Clear r6
orr r6, r6, r1, lsl COL_3  ; Set only Column 3        !!!!!
str r6, [r5]               ; Write the pattern to the address in r5
c
  

*/