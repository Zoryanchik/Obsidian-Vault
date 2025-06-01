								**Question

Which instruction is represented by the following binary word: 0xe1a0900c? What is the opcode, the destination register, the first operand register, and the immediate value?
Answer

Converting a **hexadecimal number** like `0xE1A0900C` into **binary** is straightforward. Let’s go step by step.
![[Pasted image 20250314230705.png]]![[Pasted image 20250314230741.png]]
		Condition: 1110 после кондитиона скип два нуля
		Immediate operand: if 0 second operand register if 1 so imediate value ex 10
		 Opcode: 1 101 (MOV)
		 S: 0 no set flag updated (no cpsr)
		 Rn: 0000   not usedbc mov
		 Destination register: 1001 (r9)
		 Second operand register: 1100 (r12)
		 instruction: mov r9, r12
![[Pasted image 20250314231723.png]]
Serialize the instruction cmp r9, #10 into a 32-bit word. What is the binary representation of the instruction? Assume the condition field is 1110 (AL - Always). What is the opcode field, the operand field, and the immediate field?

| Cond (4) | 00 (2) | Opcode (4) | S (1) | Rn (4) | Rd (4) | Operand2 (12) |

Condition: 1110 (AL - Always)
Because we have #10 its immediate value then our
Immediate flag: 1
Opcode: 1010 (CMP)
S: 1 bc cmp
![[Pasted image 20250314233616.png]]
Rn first
rd destinatin
Immediate value(#10) 0000 0000 0000 1010

Binary instruction: 1110 0011 0101 1001 0000 0000 0000 1010 -> 0xe359000a