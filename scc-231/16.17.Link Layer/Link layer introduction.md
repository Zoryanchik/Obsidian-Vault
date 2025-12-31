| **Feature**        | **Link Layer (Layer 2)**                    | **Network Layer (Layer 3)**                 |
| ------------------ | ------------------------------------------- | ------------------------------------------- |
| **Primary Goal**   | Communication within a local network (LAN). | Communication between different networks.   |
| **Addressing**     | **MAC Address** (Hardware-based/Static).    | **IP Address** (Logical/Assigned).          |
| **Data Unit**      | **Frame**                                   | **Packet**                                  |
| **Primary Device** | **Switch**                                  | **Router**                                  |
| **Scope**          | "Hop-to-hop" (direct neighbors).            | "End-to-end" (source to final destination). |
![[Pasted image 20251231142535.png]]![[Pasted image 20251231142633.png]]![[Pasted image 20251231142852.png]]![[Pasted image 20251231143013.png]]![[Pasted image 20251231143218.png]]![[Pasted image 20251231143442.png]]![[Pasted image 20251231143553.png]]![[Pasted image 20251231143921.png]]![[Pasted image 20251231144134.png]]![[Pasted image 20251231144339.png]]![[Pasted image 20251231144447.png]]![[Pasted image 20251231144501.png]]### The Core Goal

The sender wants to find a remainder **R** (the CRC) that, when appended to the data, makes the entire message exactly divisible by a predetermined divisor **G** (the Generator).

The formula shown in the image, $D \cdot 2^r \text{ XOR } R = nG$, means:

- **D**: The original data bits (e.g., `101110`).
    
- **$2^r$**: Shifts the data left by **r** bits to make room for the CRC. In the image, $r=3$, so three zeros are added to the end of the data.
    
- **G**: The generator polynomial agreed upon by both sender and receiver.
    
- **R**: The calculated remainder that will be sent along with the data.
    

---

### Step-by-Step Logic of the Example

The calculation uses **Modulo-2 Arithmetic**, where addition and subtraction are replaced by the **XOR** (Exclusive OR) operation. This means there are **no carries or borrows**.

1. **Preparation**: The data `101110` is "padded" with three zeros (since $r=3$), becoming `101110000`.
    
2. **Binary Division**: We divide this padded data by the generator **G** (`1001`).
    
    - If the leftmost bit is **1**, we perform an XOR with the generator.
        
    - If the leftmost bit is **0**, we XOR with zeros.
        
3. **Finding the Remainder**: The process repeats bit-by-bit until you reach the end of the data. The final result at the bottom, `011`, is the **remainder R**.
    
4. **Final Code**: The sender transmits the original data followed by this remainder: `101110 011`.