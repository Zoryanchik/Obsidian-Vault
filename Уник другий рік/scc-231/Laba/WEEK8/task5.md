![[Pasted image 20260103211006.png]]![[Pasted image 20260103211014.png]]Based on the OSPF path selection principles and the link costs established in the previous questions (where the standard link cost was determined to be **10**), here are the answers.

### **Question 17**

**Using traceroute output, select the path used when host HomePC pings host telnet, after you modify the link cost in router2.**

- **Answer:** **d. homePC -> router1 -> router3 -> router2 -> telnet**
    
- **Reasoning:**
    
    - **Goal:** The task involves increasing the cost of the direct link between Router1 and Router2 (likely to 100, as hinted in subsequent options).
        
    - **Decision:** OSPF compares the two available paths:
        
        1. **Direct (Modified):** Cost **110** (100 for link + 10 for stub).
            
        2. **Indirect (via Router3):** Cost **30** (10 to R3 + 10 to R2 + 10 to Telnet).
            
    - **Result:** Since $30 < 110$, OSPF installs the path via Router3.
        

### **Question 18**

**After you update the path cost on router1, what is the cost to reach subnet 10.0.5.0/24 from router1?**

- **Answer:** **b. 30**
    
- **Reasoning:**
    
    - The routing table always displays the metric of the _best_ (lowest cost) path.
        
    - With the direct link set to a high cost (100), Router1 switches to the path via Router3.
        
    - **Calculation:**
        
        - Router1 $\rightarrow$ Router3 (Cost **10**)
            
        - Router3 $\rightarrow$ Router2 (Cost **10**)
            
        - Router2 $\rightarrow$ Web/10.0.5.0 (Cost **10**)
            
        - **Total:** $10 + 10 + 10 = \mathbf{30}$.
            

### **Question 19**

**After applying the interface updated cost, use router2 terminal and check what is the cost to reach subnet 10.0.0.0/24 from router2.**

- **Answer:** **c. 30**
    
- **Reasoning:**
    
    - Similar to Question 18, traffic returning from Router2 to the HomePC subnet (10.0.0.0/24) will also avoid the expensive direct link.
        
    - **Calculation:**
        
        - Router2 $\rightarrow$ Router3 (Cost **10**)
            
        - Router3 $\rightarrow$ Router1 (Cost **10**)
            
        - Router1 $\rightarrow$ LAN/10.0.0.0 (Cost **10**)
            
        - **Total:** $10 + 10 + 10 = \mathbf{30}$.
            
    - _(Note: Option A [110] represents the cost of the path you are trying to avoid)._
        

### **Question 20**

**You want to prevent a path from being used without removing it entirely. What should you set the OSPF cost to?**

- **Answer:** **a. A very high value like 1000**
    
- **Reasoning:**
    
    - **Traffic Engineering:** Setting a high cost (metric) makes a link less desirable than other lower-cost paths.
        
    - **Backup Link:** By doing this, the link remains "Up" and operational. If the primary (low cost) cable is cut, OSPF will automatically failover to this high-cost link because it becomes the _only_ path available.
        
    - _Removing the interface (Option B)_ would prevent it from ever being used, even in an emergency. _Setting it to 1 (Option C)_ would make it the preferred path.