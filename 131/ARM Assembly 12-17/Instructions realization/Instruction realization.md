![[Pasted image 20250314224830.png]]
- **Condition Field (Bits 31-28)**
    
    - A **4-bit field** that determines under what condition the instruction executes.
    - Common conditions:
        - `0000` → Equal (EQ)
        - `0001` → Not Equal (NE)
        - `1010` → Greater than or equal (GE)
        - `1100` → Greater than (GT)
        - `1110` → Always (AL)
- **Opcode Field (Bits 27-21)**
    
    - **8-bit field** that defines the operation (addition, subtraction, logical operations, etc.).
    - Some examples:
        - `0000` → AND
        - `0010` → SUB (Subtract)
        - `0100` → ADD (Addition)
        - `1101` → MOV (Move)
        - `1110` → BIC (Bit Clear)
- **Operand Field (Bits 20-12)**
		    4 bit
    - Includes:
        - **Destination Register (Rd)**
        - **First Operand Register (Rn)**
        - **Set Condition Codes (S-bit)** → Determines if flags in the CPSR register are updated.
- **Operand 2 Field (Bits 11-0)**
    
    - Specifies the **second operand** for the instruction.
    - Two possible formats:
        - **Register Operand** → Uses a **shifted register value**.
        - **Immediate Operand** → Uses an **immediate value with rotation**.
- **Immediate Operand Encoding**
    
    - **Bit 25** (I-bit) determines whether Operand 2 is:
        - `0` → Register (`Rm`) with optional shift.
        - `1` → Immediate value with rotation.
- **Shifting and Rotation**
    
    - If **Operand 2 is a register**, shift operations can be applied (Logical Shift Left (LSL), Logical Shift Right (LSR), etc.).
    - If **Operand 2 is an immediate**, an 8-bit immediate value is rotated before use.


