![[Pasted image 20251231161712.png]]Based on the revision slide provided, here are the answers to the three networking questions.

---

### 1. Address Space Sizes

The size of an address space is determined by the number of bits used for the address ($2^n$, where $n$ is the number of bits).

- **MAC Address Space:** MAC addresses are **48 bits** long.
    
    - Size: $2^{48} \approx 281,474,976,710,656$ (approx. 281 trillion addresses).
        
- **IPv4 Address Space:** IPv4 addresses are **32 bits** long.
    
    - Size: $2^{32} \approx 4,294,967,296$ (approx. 4.3 billion addresses).
        
- **IPv6 Address Space:** IPv6 addresses are **128 bits** long.
    
    - Size: $2^{128} \approx 3.4 \times 10^{38}$ (340 undecillion addresses).
        

---

### 2. MAC Address Bundle Longevity

**The Problem:**

- Total MAC address bits: 48.
    
- Fixed bits (Organizationally Unique Identifier - OUI): First half = 24 bits.
    
- Available bits for the manufacturer: Remaining 24 bits.
    
- Production rate: 1,000,000 adapters/year.
    

**The Calculation:**

1. Calculate total unique addresses in one chunk:
    
    Since 24 bits are available for the manufacturer to assign, the total number of unique addresses is $2^{24}$.
    
    $$2^{24} = 16,777,216 \text{ addresses}$$
    
2. Calculate longevity:
    
    $$ \frac{16,777,216 \text{ addresses}}{1,000,000 \text{ adapters/year}} \approx 16.77 \text{ years}$$
    

**Answer:** The chunk will last for approximately **16 years and 9 months**.
![[Pasted image 20251231162205.png]]
### 3. Broadcast LAN Behavior (Nodes A, B, and C)

This question tests your understanding of Network Interface Card (NIC) hardware filtering and the interaction between the Data Link Layer and the Network Layer.

**Scenario 1: A sends unicast frames to B**

- **Will C's adapter process these frames?** **Yes, but only partially.** On a shared broadcast medium (like a bus or a hub, or wireless), the electrical signals reach C's adapter. C's adapter will read the frame header to inspect the Destination MAC address. However, upon seeing that the destination address (B) does not match its own address (C), the hardware will discard the frame. _(Note: If C is in "promiscuous mode," it would process everything, but in standard operation, it filters based on MAC)._
    
- **Will C's adapter pass the IP datagrams to the network layer?** **No.** Because the destination MAC address did not match C's MAC address, the adapter discards the frame at the physical/link layer interface. It does not extract the payload (the IP datagram) and interrupt the CPU to pass it up the stack.
    

**Scenario 2: A sends frames to the MAC Broadcast Address**

- **How do the answers change?**
    
    - **Processing:** C's adapter will examine the destination MAC address and see that it is the Broadcast Address (`FF:FF:FF:FF:FF:FF`). NICs are hardcoded to accept broadcast frames.
        
    - **Passing to Network Layer:** Since the address is accepted, C's adapter **will** pass the payload (the IP datagram) up to the Network Layer (IP) for further processing.

![[Pasted image 20251231162304.png]]Based on the networking concepts presented in the slide, here is the answer to the revision question.

### Answer: No (Under Normal Circumstances)

Under standard networking conditions, it is **not possible** for the same MAC address to appear in both of the router's ARP tables.

Here is the breakdown of why:

**1. MAC Addresses are Globally Unique** By definition, MAC addresses are unique identifiers burned into the network interface card (NIC) by the manufacturer. No two network adapters in the world are supposed to have the same MAC address.

- The hosts on the left network (111.x.x.x) are physically different devices from the hosts on the right network (222.x.x.x).
    
- Therefore, the set of MAC addresses on the left is entirely distinct from the set of MAC addresses on the right.
    

**2. ARP Tables are Local to the Network Segment** An ARP (Address Resolution Protocol) table maps **IP addresses** to **MAC addresses** for devices on the _local_ link only.

- **Module 1 (Left):** Its ARP table will only contain entries for the devices connected to the 111.111.111.x subnet.
    
- **Module 2 (Right):** Its ARP table will only contain entries for the devices connected to the 222.222.222.x subnet.
    

Since the devices are different on each side, and their MAC addresses are unique, there is no overlap between the tables.

![[Pasted image 20251231162602.png]]
### Revision Question (3)

**1. A sender wants to transmit the data 1101011 using the generator 1011. Compute the CRC remainder.**

To find the CRC remainder, we append zeros to the data (degree of generator is 3, so append three 0s) and perform binary division (XOR).

- **Data:** `1101011`
    
- **Generator:** `1011`
    
- **Augmented Data:** `1101011000`
    

**Calculation:**

Plaintext

```
              1100001
        _____________
  1011 ) 1101011000
         1011
         ----
          1100
          1011
          ----
           1111
           1011
           ----
            1001
            1011
            ----
             0100
             0000
             ----
              1000
              1011
              ----
               0110
               0000
               ----
                110  <-- Remainder
```

**Answer:** The CRC remainder is **110**.

---

**2. A receiver received the codeword 11010101011 generated using the generator 1011. Are the received data error-free?**

To check for errors, we divide the received codeword by the generator. If the remainder is `0`, the data is error-free. If non-zero, an error occurred.

- **Codeword:** `11010101011`
    
- **Generator:** `1011`
    

**Calculation:**

Plaintext

```
              11001110
        ______________
  1011 ) 11010101011
         1011
         ----
          1100
          1011
          ----
           1111
           1011
           ----
            1000
            1011
            ----
             0111
             0000
             ----
              1110
              1011
              ----
               1011
               1011
               ----
                0001  <-- Remainder
```

**Answer:** The remainder is **001** (non-zero). Therefore, **No**, the received data is **not** error-free; an error has been detected.