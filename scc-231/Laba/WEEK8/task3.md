![[Pasted image 20260103204235.png]]![[Pasted image 20260103204459.png]]### **Question 3.1: How many OSPF neighbors does router1 have? What are their router IDs and states?**

- **Number of Neighbors:** **2**
    
    - **Reasoning:** `router1` has physical connections to `router2` and `router3`. It also connects to `switch1` (the host LAN), but typical hosts (PC1, PC2) do not run OSPF, so no adjacency forms there.
        
- **Neighbor Router IDs:**
    
    - **1.1.1.2** (This is `router2`).
        
    - **1.1.1.3** (This is `router3`).
        
- **States:**
    
    - The state should be **Full**. (Depending on the DR/BDR election on the Ethernet segment, you might see `Full/DR` or `Full/Backup`, but "Full" indicates a complete adjacency).
        

### **Question 3.2: What is the “dead time” for each neighbor? How does this relate to the hello interval configured in the OSPF configuration?**

- **Dead Time:** **30 seconds**.
    
    - When you view neighbors (`show ip ospf neighbor`), you will see a countdown timer in the "Dead Time" column. It starts at 30 seconds and counts down until the next Hello packet is received, at which point it resets to 30.
        
- **Relationship:**
    
    - The configuration explicitly sets the `dead-interval` to **30** and the `hello-interval` to **5**.
        
    - In this specific lab, the dead interval is configured to be **6 times** the hello interval (30 / 5 = 6). This is slightly higher than the standard Cisco default (which is usually 4x), making the network more tolerant of missed packets.
        

### **Question 3.3: What is the OSPF cost for each interface on router1? How does OSPF determine the cost of a link by default?**

- **Cost Determination:**
    
    - By default, OSPF calculates cost using the formula:
        
        $$Cost = \frac{\text{Reference Bandwidth}}{\text{Interface Bandwidth}}$$
        
    - The default Reference Bandwidth is usually 100 Mbps ($10^8$).
        
- **Cost on Router1:**
    
    - Since no manual `ip ospf cost` command exists in the configuration files, the router calculates this dynamically.
        
    - In Mininet, virtual Ethernet interfaces often report 10 Gbps or similar high speeds. If the bandwidth is higher than the reference (100Mbps), the cost defaults to **1**. If the interfaces report 10Mbps (common in older emulations), the cost would be **10**. (You can verify this in the lab with `show ip ospf interface`).
        

### **Question 3.4: Draw a diagram showing all OSPF adjacencies. Is every router adjacent to every other router? Why or why not?**

- **Diagram Description:**
    
    - Imagine a **Triangle**.
        
    - **Top:** Router 1
        
    - **Right:** Router 2
        
    - **Bottom:** Router 3
        
    - Lines connect all three corners (R1-R2, R2-R3, R3-R1).
        
- **Is every router adjacent to every other router?**
    
    - **Yes.** In this specific topology, every router has a direct physical link to every other router. Since they are all in **Area 0** and configured correctly, they form a "Full Mesh" of adjacencies.
        
    - **Why:** Adjacencies only form over direct links. Because `router1` connects to `router2`, `router1` connects to `router3`, and `router2` connects to `router3`, the graph is fully connected.

Based on the `topology.py` file and standard OSPF behavior, here are the answers to the questions.

### **Question 9**

**How many OSPF neighbours should router2 have when all links are operational?**

- **Answer:** **c. 2**
    
- **Evidence:**
    
    - **Neighbor 1:** Router 2 connects directly to **Router 1** via `router2-eth0`.
        
    - **Neighbor 2:** Router 2 connects directly to **Router 3** via `router2-eth2`.
        
    - The other connections (`router2-eth3` to `web` and `router2-eth1` to `switch2`) connect to **hosts** (PCs/Servers), which do not participate in OSPF.
        

### **Question 10**

**When running the command `show ip ospf interface` What is the reported link speed on every interface?**

- **Answer:** **b. 10000 Mbps**
    
- **Reasoning:**
    
    - The topology script uses standard Mininet links without defining a specific bandwidth limit (`bw` parameter).
        
    - Mininet uses Linux virtual Ethernet (veth) pairs for these links. These virtual interfaces typically report a speed of **10Gbps (10000 Mbps)** to the operating system and FRR. This is also why the OSPF cost usually defaults to **1** (Reference 100 Mbps / 10000 Mbps < 1, which rounds up to 1).
        
![[Pasted image 20260103205314.png]]
### **Question 11**

**How many neighbours are accessible via the link router2-eth0 on router2?**

- **Answer:** **d. 1**
    
- **Evidence:**
    
    - According to `topology.py`, the link is defined as: `self.addLink(router1, router2, ... intfName2='router2-eth0' ...)`.
        
    - This is a **direct point-to-point connection** between Router 2 and Router 1. There are no switches or hubs in between, so Router 1 is the only possible neighbor on that specific interface.
        
**LSA** stands for **Link-State Advertisement**.

In OSPF, an LSA is the fundamental unit of communication. It is a small packet of information that a router sends out to announce its presence and the status of its links to the rest of the network.

Think of an LSA as a **"Status Update"** or a **"Puzzle Piece."**


### **Question 12**

**How does OSPF detect when an LSA is newer than one already in the database?**




- **Answer:** **a. By comparing sequence numbers**
    
- **Reasoning:**
    
    - This is a fundamental OSPF mechanism. Every Link State Advertisement (LSA) contains a 32-bit **sequence number**.
        
    - When a router receives an LSA, it compares the sequence number to the one in its local database. If the received number is higher, the update is considered newer and is processed.

Here is a more detailed explanation of how OSPF uses sequence numbers to keep track of network updates.

### The "Version Control" of OSPF

Think of the LSA Sequence Number like a **version number** on a document (v1.0, v1.1, v1.2).

In a network, updates (LSAs) travel via different paths and can arrive out of order. A router might receive "Version 5" of an update from Neighbor A, and milliseconds later receive "Version 4" of the same update from Neighbor B (because it took a longer path).

To prevent the router from overwriting new information with old information, OSPF looks at the **Sequence Number field** in the LSA header.

### How the Numbering Works

OSPF uses a **Signed 32-bit Integer** for these numbers.

- **Starting Value:** `0x80000001` (This looks like a huge negative number in signed math, but OSPF treats it as the starting point, called _InitialSequenceNumber_).
    
- **Maximum Value:** `0x7FFFFFFF` (The maximum positive signed integer).
    
- **Incrementing:** Every time a router needs to update its LSA (e.g., a link goes down, or the regular 30-minute refresh timer hits), it simply adds **+1** to the sequence number.
    

### The Decision Logic

When a router receives an LSA, it compares it against the copy it already has in its Link-State Database (LSDB):

1. **New LSA has a HIGHER sequence number:**
    
    - **Verdict:** This is new information.
        
    - **Action:** The router accepts the LSA, updates its database, runs the SPF algorithm (if necessary), and floods the LSA to other neighbors.
        
2. **New LSA has a LOWER sequence number:**
    
    - **Verdict:** This is old information (outdated).
        
    - **Action:** The router ignores the update. It may send its _own_ (newer) copy back to the neighbor to help update them.
        
3. **New LSA has the SAME sequence number:**
    
    - **Verdict:** Duplicate information.
        
    - **Action:** The router ignores it (specifically, it treats it as an implicit acknowledgment).
        

### Advanced: What if the Sequence Numbers are the same?

If the sequence numbers are identical, OSPF has a strict tie-breaker order to check if one is actually "better" or newer:

1. **Check the Checksum:** If sequence numbers match, the LSA with the **higher checksum** is considered newer.
    
2. **Check the Age:** If sequence numbers and checksums match, check the `LS Age` field.
    
    - If one LSA has an age of `MaxAge` (3600 seconds, meaning "delete me"), it is prioritized.
        
    - Otherwise, the difference in age is usually ignored unless it is significant (more than 15 minutes), to prevent constant updates due to slight timing differences.
        

### Summary Example

- **Event 1:** Router A's link fails. It sends LSA (Seq: `0x80000005`).
    
- **Event 2:** Router B receives it and updates its map.
    
- **Event 3:** Router A's link comes back up. It sends LSA (Seq: `0x80000006`).
    
- **Scenario:** If Router B receives packet #6 first, and then packet #5 arrives late (due to network lag), Router B sees that `5 < 6` and immediately discards packet #5.