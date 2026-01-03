![[Pasted image 20260103211730.png]]
![[Pasted image 20260103212036.png]]![[Pasted image 20260103211740.png]]### Task 6 Reflective Questions
![[Pasted image 20260103212629.png]]
- **Question 6.1:** How many packets were lost during convergence? Approximately how long did OSPF take to reconverge?
- **Question 6.2:** What is the new path from router1 to web? How does it differ from the original path?
- **Question 6.3:** What happened to the neighbor relationship with router2 while the link is down? Is router2 still reachable?
- **Question 6.4:** How long does it take for the neighbor adjacency to re-establish? Does the route revert to the original path?


Here are the answers to the **Task 6 Reflective Questions**, based on the OSPF principles and the specific topology provided in your lab material.

These answers reflect what happens when you administratively shut down the link between Router 1 and Router 2 (`router1-eth1`).

### Task 6: OSPF Convergence and Failure Recovery

#### Question 6.1: How many packets were lost during convergence? Approximately how long did OSPF take to reconverge?

- **Packet Loss:** You likely observed a loss of **very few packets (typically 1–4 packets)** if you were running a standard `ping` (which sends one packet per second).
    
- **Convergence Time:** The reconvergence likely took **only a few seconds (approx. 1–5 seconds)**.
    
- **The "Why":** In this specific task, you used the `shutdown` command. This is an "administrative down" event. The Linux kernel on Router 1 immediately detects the interface state change and notifies the OSPF process (`ospfd`). Router 1 immediately triggers an LSA update to flood the network, telling other routers the link is gone. This bypasses the "Dead Interval" timer (configured to 30s in your lab), resulting in very fast convergence.
    
    - _Note:_ If the failure had been "silent" (e.g., a cable cut where the interface stays "up" but data stops), OSPF would have waited for the **Dead Interval (30 seconds)** before declaring the neighbor down, resulting in much higher packet loss.
        

#### Question 6.2: What is the new path from router1 to web? How does it differ from the original path?

- **The New Path:** `Router 1 -> Router 3 -> Router 2 -> Web`
    
    - This is confirmed by the routing table output in the text: `via 10.0.3.1, router1-eth2`.
        
- **The Difference:**
    
    - **Hop Count:** The path is longer. It adds an extra hop (Router 3) instead of going directly to Router 2.
        
    - **Cost:** The metric (cost) has increased.
        
        - _Original Cost:_ 20 (10 for the link to R2 + 10 for the link to Web).
            
        - _New Cost:_ 30 (10 to R3 + 10 from R3 to R2 + 10 from R2 to Web).
            
    - **Latency:** You would likely see a slight increase in milliseconds in your ping results due to the extra processing hop and wire distance.
        

#### Question 6.3: What happened to the neighbor relationship with router2 while the link is down? Is router2 still reachable?

- **Neighbor Relationship:** The OSPF neighbor relationship (adjacency) typically moves to the **DOWN** state for that specific interface. It disappears from the `show ip ospf neighbor` list on the interface `router1-eth1`.
    
- **Reachability:** **Yes, Router 2 is still reachable.**
    
    - Although the _direct_ link is down, OSPF has found an alternative path. Router 1 can still reach Router 2's Loopback ID or internal interfaces by routing packets through Router 3.
        
    - This highlights the resilience of dynamic routing: "Neighbor down" does not necessarily mean "Destination unreachable."
        

#### Question 6.4: How long does it take for the neighbor adjacency to re-establish? Does the route revert to the original path?

- **Re-establishment Time:** When you bring the interface back up (`no shutdown`), it typically takes **5 to 10 seconds** to re-establish.
    
    - The routers must exchange Hello packets (Hello Interval is 5s), progress through the states (Init $\to$ 2-Way $\to$ ExStart $\to$ Exchange $\to$ Loading), and synchronize their databases before reaching the `Full` state.
        
- **Route Reversion:** **Yes, the route reverts to the original path.**
    
    - OSPF is deterministic and aggressive about using the Shortest Path First (SPF).
        
    - As soon as the direct link (Cost 10) is restored, the total cost to reach the Web server becomes 20 again. Since 20 is less than the backup path cost of 30, OSPF immediately updates the routing table to use the direct link.
        

---

### Key Takeaway for your Lab

This task demonstrates the difference between **Physical Interface Failure** (instant detection by kernel $\to$ fast OSPF update) and **Protocol Adjacency Failure** (requires Dead Timers). Because you used `shutdown`, you witnessed the faster, event-driven convergence of OSPF.

**Would you like me to explain how to interpret the FRR logs (Task 7) to see the exact timestamps of these state changes?**




Here are the answers to your reflective quiz questions, formatted for clarity and readability.

---

### **Question 21**

**Question text:** What happens when you bring down an interface using the `shutdown` command in vtysh?

- **Correct Answer:** **b. The interface goes down, and OSPF withdraws routes advertised through it**
    

> Reasoning:
> 
> The shutdown command is an administrative action. The router's kernel immediately flags the interface as "down," which triggers the OSPF process to remove any networks associated with that interface from its database. It then immediately floods an updated Link State Advertisement (LSA) to neighbors to withdraw those routes, without waiting for timers to expire.

---

### **Question 22**

**Question text:** In our lab exercise, when you set the interface router1-eth1 state to down on router1, what happens to the OSPF neighbour state on router2?

- **Correct Answer:** **b. It immediately transitions to "Down".**
    

> Reasoning:
> 
> In this specific Mininet topology, the routers are connected via virtual Ethernet pairs which simulate a direct cable. When you shut down the interface on Router 1, the "carrier signal" on Router 2's corresponding interface drops. Router 2's kernel detects this physical link loss instantly and notifies OSPF, causing the neighbor relationship to tear down immediately.
> 
> _(Note: If there were an unmanaged switch between them that stayed powered on, Router 2 would not detect the physical loss and would instead have to wait for the Dead Interval timer (Option D).)_

---

### **Question 23**

**Question text:** In the failure lab scenario, if the direct link between router1 and router2 fails, which path will traffic from pc1 to web (10.0.5.2) take?

- **Correct Answer:** **d. router1 → router3 → router2 → web**
    

> Reasoning:
> 
> With the direct path (R1 → R2) unavailable, OSPF recalculates the Shortest Path First (SPF) using the remaining links.
> 
> - **Step 1:** Router 1 connects to Router 3 (cost 10).
>     
> - **Step 2:** Router 3 connects to Router 2 (cost 10).
>     
> - **Step 3:** Router 2 connects to the Web Server (cost 10).
>     
> 
> This becomes the only valid path to the destination.

---

### **Question 24**

**Question text:** In a typical production network, network administrators use a hello interval of 10 seconds and a dead interval of 40s. Why?

- **Correct Answer:** **c. Higher HELLO intervals reduce the router's compute overheads and improve scalability.**
    

> Reasoning:
> 
> There is a trade-off between speed and stability:
> 
> - **Fast Hello timers (e.g., 1s):** Detect failures quickly but generate huge amounts of control plane traffic and require high CPU usage to process. This limits how many neighbors a router can handle.
>     
> - **Standard Hello timers (10s):** Keep the network stable and reduce the CPU load (overhead) on routers, allowing the network to scale larger, even though failure detection takes longer (40s).
>     

---

**Would you like me to create a quick summary table comparing the "Administrative Down" vs. "Dead Interval" failure modes?**