![[Pasted image 20250210032618.png]]
![[Pasted image 20250210032637.png]]
![[Pasted image 20250210032707.png]]![[Pasted image 20250210032732.png]]![[Pasted image 20250210032748.png]]![[Pasted image 20250210032827.png]]  
Why, if we go from 64 bits to 48 bits, why is this equivalent to using the lower half and the high half of the full memory? Because if you remove the first, if you ignore the first four digit hexadecimal digits. mmediately you drop from 16 hexadecimal to 12, which is equivalent to 48 bits. so from 0 to 7
So the next one is. So if you add one here, everything will become zero and the same one will become eight.
But the virtually what happens is you go from seven on that on and all lives to the next to this, which is eight and all zeros.
ht. So from six, this is the way that 64, uh, addresses, 64 bit addresses, has been mapped into 48 bit addresses.

In many modern processors (e.g., x86-64 architecture), while the virtual address space is technically **64 bits**, only **48 bits** are used for actual addressing. This is done for the following reasons:

#### a. **Physical Constraints**

- **64 bits of addressing** would allow access to 2642^{64}264 bytes of memory, which equals **16 exabytes**.
- Current systems do not need such an enormous address space because most hardware (RAM and storage) operates at much smaller scales (e.g., terabytes).

#### b. **Practicality**

- Using the full 64-bit address space would require larger page tables and more memory to store these tables. Reducing the address space to 48 bits makes the memory management more efficient while still providing 2482^{48}248, or **256 terabytes**, of addressable space.

#### c. **Simplification of Hardware**

- Circuitry required for handling full 64-bit addresses is more complex and expensive. Limiting the address space reduces this complexity.

![[Pasted image 20250210033320.png]]
Has a particular logic. So if we want to store this integer where under this address, right ff00005, we know that only one byte can be stored.But we give an address and say okay, store this full byte in own to this address. It means that the first byte will be stored and then the next three bytes will follow.When we say little endian, it means that the first byte that will be stored is the little end, that least significant byte, which is 78.