![[Pasted image 20260103205640.png]]![[Pasted image 20260103205649.png]]![[Pasted image 20260103205701.png]]![[Pasted image 20260103205711.png]]![[Pasted image 20260103205720.png]]![[Pasted image 20260103205727.png]]Based on the topology and OSPF concepts we have explored, here are the answers to the **Task 4 Reflective Questions** shown in your image.

### **Question 4.1**

**How many Router LSAs are in the database of router2? How many links are advertised by router1, based on the LSA table content in router2?**

- **Number of Router LSAs:** **3**.
    
    - **Reasoning:** In a single-area OSPF network (Area 0), every router generates exactly one "Router LSA" (Type 1 LSA) to describe itself. Since there are three routers in the topology (Router1, Router2, and Router3), the database on _any_ router (including Router2) will contain exactly **3** Router LSAs.
        
- **Links advertised by Router1:** **3 Links**.
    
    - **Reasoning:** Router1 advertises every interface enabled for OSPF. Looking at the topology, Router1 has three active connections:
        
        1. The Stub Network (LAN) to the PCs (`10.0.0.0/24`).
            
        2. The Point-to-Point connection to Router2 (`10.0.1.0/24`).
            
        3. The Point-to-Point connection to Router3 (`10.0.3.0/24`).
            

---

### **Question 4.2**

**What information does this LSA contain? How many links does router router1 advertise?**

- **Information in a Router LSA:**
    
    - **Link ID / Data:** Identifies the network or the neighbor router.
        
    - **Link Type:** Describes the connection (e.g., _Stub_ for the LAN, _Transit_ or _Point-to-Point_ for links to other routers).
        
    - **Metric (Cost):** The cost to reach that specific neighbor or network (usually 1 or 10 in this lab).
        
- **Links Advertised:** As noted above, **3 links**. (It describes the topology from Router1's perspective: "I am connected to R2, R3, and my local LAN").
    

---

### **Question 4.3**

Which routes are marked with ‘O’ (OSPF)? What is the metric for the route to 10.0.4.0/24? Through which next-hop(s) is it reachable?

(Note: This question assumes you are looking at Router1's routing table, as Router2 and Router3 are directly connected to 10.0.4.0).

- **Routes marked with 'O':**
    
    - **10.0.2.0/24:** (Router2's LAN).
        
    - **10.0.4.0/24:** (The link between Router2 and Router3).
        
    - **10.0.5.0/24:** (The Web Server network).
        
- **Metric for 10.0.4.0/24:** **2** (assuming interface cost is 1).
    
    - _Calculation:_ Router1 $\rightarrow$ Router2 (Cost 1) $\rightarrow$ Link 10.0.4.x (Cost 1) = **2**.
        
- **Next-Hops:**
    
    - Since Router1 forms a triangle with R2 and R3, the cost to reach the link _between_ R2 and R3 is identical via either side (1 hop to R2, or 1 hop to R3).
        
    - OSPF will likely install **two next-hops** (Equal Cost Multi-Path / ECMP):
        
        1. **10.0.1.1** (via Router2)
            
        2. **10.0.3.1** (via Router3)
            

---

### **Question 4.4**

**What is the path from router1 to the web server (10.0.5.2)? Does it match what you expected from the routing table?**

- **Path:** **Router1 $\rightarrow$ Router2 $\rightarrow$ Web Server**.
    
- **Next Hop:** **10.0.1.1** (Router2).
    
- **Reasoning:**
    
    - **Path via R2:** Cost 1 (to R2) + Cost 1 (to Web) = **Total Cost 2**.
        
    - **Path via R3:** Cost 1 (to R3) + Cost 1 (to R2) + Cost 1 (to Web) = **Total Cost 3**.
        
    - OSPF chooses the lowest cost, so it goes directly to Router2.
        
- **Does it match?** Yes. The routing table will show the next hop as `10.0.1.1`, and a `traceroute` would show `10.0.1.1` followed by `10.0.5.2`.

Based on the OSPF concepts and the specific "Cost = 10" logic derived from the options provided (where the cost to a neighbor's LAN is 20), here are the correct answers.

### **Question 13**

**If router1's LSA shows "Number of Links: 3", what does this represent?**

- **Answer:** **c. Three network segments advertised in the LSA**
    
- **Reasoning:**
    
    - In an OSPF Router LSA (Type 1), the "Link Count" refers to the number of active OSPF interfaces or "Link descriptions" the router is sharing.
        
    - For Router 1, these three segments correspond to:
        
        1. The Stub Network (The LAN with PC1/PC2: `10.0.0.0/24`).
            
        2. The Point-to-Point connection to Router 2 (`10.0.1.0/24`).
            
        3. The Point-to-Point connection to Router 3 (`10.0.3.0/24`).
            
    - While these happen to use three cables, the LSA is describing the _logical network segments_.
        

### **Question 14**

**In OSPF, what is a "Stub Network"?**

- **Answer:** **c. A network segment that connects hosts but isn't used for transit between routers**
    
- **Reasoning:**
    
    - In OSPF terminology, a "Stub Network" link type describes a dead-end segment where the router sends data _to_, but does not expect to route traffic _through_ to reach another router.
        
    - The LAN connected to Router 1 (containing `homePC`, `pc1`) is a perfect example: traffic goes there to terminate at a host, not to pass through to another part of the network.
        

### **Question 15**

**Using the output of the command `show ip route` on router2, select what is the path cost to get from router to subnet 10.0.5.0/24?**

- **Answer:** **a. 10**
    
- **Reasoning:**
    
    - **Context from Question 16:** In Question 16 (below), the cost to a neighbor's network is **20**. This implies the cost per link in this specific lab setup is **10** (10 + 10 = 20).
        
    - **Logic:** The subnet `10.0.5.0/24` is directly connected to Router 2 (the web server link). In OSPF, the cost to a directly connected stub network is simply the cost of that interface. Since we established the link cost is 10, the cost is **10**.
        
    - _(Note: While strictly "Connected" routes often have a metric of 0 in the routing table, OSPF labs typically ask for the OSPF metric assigned to the link, which fits the pattern of options provided: 10, 20, 40)._
        

### **Question 16**

**What is the path cost to get to network 10.0.0.0/24, from router2?**

- **Answer:** **c. 20**
    
- **Reasoning:**
    
    - **Destination:** `10.0.0.0/24` is the LAN attached to Router 1.
        
    - **Path:** Router 2 $\rightarrow$ Router 1 $\rightarrow$ LAN.
        
    - **Calculation:**
        
        1. Router 2 $\rightarrow$ Router 1 Link Cost: **10**.
            
        2. Router 1 $\rightarrow$ LAN Link Cost: **10**.
            
        3. **Total Path Cost:** 10 + 10 = **20**.
            
    - If you ran `show ip route` on Router 2, you would see an entry like `O 10.0.0.0/24 [110/20]`, confirming the metric is 20.