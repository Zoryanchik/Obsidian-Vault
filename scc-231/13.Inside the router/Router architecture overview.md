![[Pasted image 20251230200807.png]]![[Pasted image 20251230200935.png]]## 1. Line Termination (Physical Layer)

This is the "entry gate."

- **What happens:** The router receives raw electrical, optical, or radio signals from the physical cable.
    
- **The Goal:** It converts these physical signals back into digital bits (0s and 1s) that the computer can understand.
    

## 2. Link Layer Protocol (Data Link Layer)

This is the "envelope opener."

- **What happens:** It handles protocols like Ethernet. It checks for errors to make sure the data wasn't corrupted during transmission and strips off the outer layer of the data "envelope."
    
- **The Goal:** To get the data ready for the actual decision-making process.
    

## 3. Lookup, Forwarding, & Queuing (Network Layer)

This is the "brain" of the input port, often called **Decentralized Switching**.

- **Lookup:** The port looks at the destination address in the packet header. It uses a local **forwarding table** (a copy of the master list) to decide which output port this packet needs to go to. This is called **"match plus action."**
    
- **Queuing:** If the "switch fabric" (the internal highway) is busy or if packets are arriving too fast, the packets wait in a line (the red bars in the image).
    
- **The Goal:** Processing everything at **'line speed'**—meaning the router works so fast that it doesn't slow down the incoming traffic.
    

---

### Why "Decentralized"?

Instead of every packet waiting for one central "boss" (the CPU) to tell it where to go, each input port has its own copy of the forwarding table. This allows the router to handle millions of packets per second simultaneously.

**Would you like me to explain what happen**
![[Pasted image 20251230201533.png]]![[Pasted image 20251230201620.png]]