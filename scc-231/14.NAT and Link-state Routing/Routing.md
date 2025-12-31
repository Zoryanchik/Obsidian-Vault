![[Pasted image 20251230221549.png]]

|**Feature**|**Forwarding (Data Plane)**|**Routing (Control Plane)**|
|---|---|---|
|**Scope**|**Local**, per-router action.|**Network-wide** process.|
|**Main Task**|Moving a packet from a router's **input link** to the appropriate **output link**.|Determining the **end-to-end path** taken by packets from source to destination.|
|**Plane**|Implemented in the **Data Plane**.|Implemented in the **Control Plane**.|
|**Logic Tool**|Uses a **Local Forwarding Table**.|Uses **Routing Algorithms** (like Dijkstra) to build tables.|

![[Pasted image 20251230221849.png]]
![[Pasted image 20251230222037.png]]![[Pasted image 20251230222258.png]]
Dijkstra’s link-state routing algorithm

![[Pasted image 20251230222417.png]]![[Pasted image 20251230222527.png]]![[Pasted image 20251230222549.png]]![[Pasted image 20251230222635.png]]  ![[Pasted image 20251230222823.png]]![[Pasted image 20251230222901.png]]![[Pasted image 20251230222912.png]]![[Pasted image 20251230222940.png]]![[Pasted image 20251230223043.png]]![[Pasted image 20251230223059.png]]![[Pasted image 20251230223135.png]]![[Pasted image 20251230223141.png]]
![[Pasted image 20251230223247.png]]- **Dijkstra's** finds the "cheapest" path.
    
- **All traffic** moves to that cheapest path.
    
- Because of the high traffic, that path becomes **expensive** (congested).
    
- In the next update, Dijkstra's sees a different path is now "cheapest" and moves **all traffic** there.
    
- The cycle repeats indefinitely.
![[Pasted image 20251230223702.png]]
![[Pasted image 20251230223717.png]]### 1. Intra-AS Routing (Intra-domain)

This refers to routing that occurs **within** a single Autonomous System.

- **Protocol Consistency:** Every router within a specific AS must use the same intra-domain routing protocol (such as OSPF or IS-IS).
    
- **Independence:** Different ASes can choose to run different intra-domain routing protocols from one another.
    
- **Gateway Routers:** These specific routers sit at the "edge" of their AS and possess physical links to routers located in other ASes.
    

### 2. Inter-AS Routing (Inter-domain)

This refers to the routing that happens **between** different Autonomous Systems.

- **Global Connectivity:** It handles how traffic is directed among different ASes to reach a final destination.
    
- **The Role of Gateways:** Gateway routers are responsible for performing inter-domain routing tasks in addition to their standard intra-domain routing duties.
![[Pasted image 20251230224022.png]]![[Pasted image 20251230224055.png]]![[Pasted image 20251230224146.png]]![[Pasted image 20251230224228.png]]
The second slide shows how OSPF specifically creates a hierarchy within one Autonomous System to keep it efficient.

- **Two-Level Hierarchy:** OSPF divides a large network into a central **Backbone (Area 0)** and several **Local Areas** (Area 1, 2, 3, etc.).![[Pasted image 20251230224311.png]]### Slide 1: Internet Approach to Scalable Routing

The first slide describes the global strategy for the Internet: treating it as a "network of networks".

- **Autonomous Systems (AS):** Routers are grouped into regions called ASes or "domains". An AS is a group of networks under a single administrative authority (like an ISP or a large university).
    
- **Intra-AS (Intra-domain) Routing:**
    
    - This is routing that happens **within** the same AS.
        
    - All routers in that AS must use the **same** protocol.
        
    - Common protocols include **RIP** (Distance Vector) and **OSPF** (Link State).
        
- **Inter-AS (Inter-domain) Routing:**
    
    - This handles routing **among different** ASes.
        
    - It relies on **Gateway Routers** (at the "edge" of an AS) that connect to other domains.
        
    - The standard protocol for this is **BGP** (Border Gateway Protocol)