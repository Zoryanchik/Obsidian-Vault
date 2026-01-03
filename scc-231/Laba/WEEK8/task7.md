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