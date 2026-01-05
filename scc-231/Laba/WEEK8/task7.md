![[Pasted image 20260103213239.png]]
![[Pasted image 20260103213524.png]]
![[Pasted image 20260103213758.png]]### Task 7 Reflective Questions

- **Question 7.1:** Find log entries related to neighbor state changes. What states does an OSPF neighbor go through before becoming “Full”?
- **Question 7.2:** What happened to the neighbor relationship between router2 and router3 once the misconfiguration was introduced? Why can’t they form an adjacency?
- **Question 7.3:** Verify that the neighbor adjacency is restored. How quickly does OSPF detect and correct this type of configuration error?

---

### **Question 7.1**

**Question text:** Find log entries related to neighbor state changes. What states does an OSPF neighbor go through before becoming “Full”?

- The Log Entry:
    
    You will typically see a log entry similar to this:
    
    %OSPF-5-ADJCHG: ... Neighbor ... from LOADING to FULL, Loading Done
    
- The States (In Order):
    
    To reach the fully functional state, the router transitions through these 7 steps:
    
    1. **Down:** No information received from the neighbor.
        
    2. **Init:** Hello packet received, but our ID is not in it yet (one-way).
        
    3. **2-Way:** Bi-directional communication established (crucial checkpoint).
        
    4. **ExStart:** Master/Slave election for database exchange.
        
    5. **Exchange:** Summary of database (DBD packets) is exchanged.
        
    6. **Loading:** Requesting specific link-state details (LSR/LSU).
        
    7. **Full:** Databases are synchronized and the router is ready to route traffic.
        

---

### **Question 7.2**

**Question text:** What happened to the neighbor relationship between router2 and router3 once the misconfiguration was introduced? Why can’t they form an adjacency?

- What Happened:
    
    The neighbor relationship broke immediately. The adjacency dropped, and the neighbor disappeared from the active list (or went to Down state).
    
- Why It Failed:
    
    OSPF is strict about adjacency requirements. For two routers to form a relationship, specific parameters in their Hello packets must match exactly.
    
    In this task, you created an Area ID Mismatch:
    
    - **Router 2** sent Hellos marked for **Area 1**.
        
    - **Router 3** expected Hellos for **Area 0**.
        
    - Because the Areas did not match, Router 3 ignored the packets, preventing the adjacency.
        

---

### **Question 7.3**

**Question text:** Verify that the neighbor adjacency is restored. How quickly does OSPF detect and correct this type of configuration error?

- Verification:
    
    Once you corrected the configuration on Router 2, the show ip ospf neighbor command would show the neighbor transitioning rapidly back to the Full state.
    
- Speed of Recovery:
    
    OSPF detects and corrects this almost immediately (typically within 5 seconds).
    
    - Unlike a physical cable break which might rely on timeouts, a configuration change generates immediate Hello packets.
        
    - As soon as Router 2 sent a Hello packet with the correct **Area 0** ID, Router 3 accepted it, and they immediately began synchronizing.
        

---

**Would you like me to tackle Task 8 (Traffic Engineering) with this same format?**



Here are the correct answers and explanations for your quiz questions.

### **Question 25**

**Question text:** Network areas are a common way for OSPF domains to scale routing in large networks. In our example, we misconfigured the area membership in a link between router1 and router2. What happens if two routers on the same link are configured in different OSPF areas?

- **Correct Answer:** **b. They cannot form an adjacency**
    

> Reasoning:
> 
> OSPF is strict about what constitutes a valid neighbor. When routers exchange Hello packets, they verify specific parameters. If any of the following do not match, the packet is ignored, and no adjacency forms:
> 
> - **Area ID** (This is the mismatch in your question)
>     
> - Subnet Mask
>     
> - Hello and Dead Intervals
>     
> - Authentication
>     

---

### **Question 26**

**Question text:** Which of the following logging lines from router1 reports the area misconfiguration problem?

- **Correct Answer:** **a. OSPF: [Y9FH4-5CVMQ][EC 134217741] interface router2-eth0:10.0.1.1: ospf_read invalid Area ID 0.0.0.1**
    

> Reasoning:
> 
> This log line explicitly identifies the root cause of the failure.
> 
> - **`ospf_read`**: The router processed an incoming packet.
>     
> - **`invalid Area ID`**: It checks the Area ID field in the Hello packet header.
>     
> - **`0.0.0.1`**: It shows that it received a packet tagged for Area 1 (which you configured), but the receiving interface was expecting Area 0 (default).
>     
> 
> _Why the others are wrong:_
> 
> - _(b)_ refers to a normal Designated Router (DR) election.
>     
> - _(c)_ and _(d)_ show the _consequence_ (adjacency going down), but option (d) specifically attributes it to an `InactivityTimer` (timeout), which happens if packets stop arriving entirely, not if they arrive with the wrong config. Option (a) is the specific error message for the mismatch.
>