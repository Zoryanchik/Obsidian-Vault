![[Pasted image 20260103202633.png]]![[Pasted image 20260103202642.png]]![[Pasted image 20260103202649.png]]### **Question 5**

**What is the OSPF router id for router2?**

- **Answer:** **d. 1.1.1.2**
    
- **Evidence:** In the file `conf/ospfd-router2.conf`, under the `router ospf` section, the configuration explicitly states: `ospf router-id 1.1.1.2`.
    

### **Question 6**

**What are the default hello and dead intervals configured in this lab?**

- **Answer:** **b. hello: 5s, dead: 30s**
    
- **Evidence:** In the configuration files (e.g., `conf/ospfd-router1.conf` or `conf/ospfd-router2.conf`), the interfaces are configured with the commands:
    
    - `ip ospf hello-interval 5`
        
    - `ip ospf dead-interval 30`.
        

### **Question 7**

**Why is the dead-interval typically set to multiple times the hello-interval?**

- **Answer:** **c. To allow multiple missing HELLOs, before declaring a neighbour down**
    
- **Reasoning:** If the Dead Interval were the same as the Hello Interval, a single lost packet (which is common in networks) would cause the neighbor relationship to drop, leading to network instability ("flapping"). Setting it to a multiple (usually 4x in standard OSPF, though 6x in this specific lab configuration) ensures that the network is robust against minor packet loss.
    

### **Question 8**

**What is the role of the zebra daemon in FRR?**

- **Answer:** **d. It manages the routing table and interfaces**
    
- **Evidence:** The lab description explicitly states: "The zebra daemon manages the routing table and interfaces, while ospfd implements the OSPF protocol." Additionally, the topology script launches `zebra` separately to handle kernel interaction.