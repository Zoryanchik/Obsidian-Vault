![[Pasted image 20260103195658.png]]![[Pasted image 20260103195728.png]]
![[Pasted image 20260103195942.png]]
![[Pasted image 20260103200204.png]]![[Pasted image 20260103195743.png]]
The text you provided is essentially a **lab briefing** describing the software architecture of a virtual router you are about to use. It explains how the router is built inside a simulation tool called Mininet.

It breaks down the router into three distinct layers: the **Control Plane** (the brains), the **Data Plane** (the muscle), and the **Interface** (how you talk to it).

Here is the explanation of each part:

### 1. The "Brains" (Control Plane)

The text explains that the router's decision-making logic is powered by **FRR**, specifically two daemons:

- **`ospfd` (The Strategist):** This program speaks the OSPF language. It chats with neighbor routers, learns the network map, and calculates the best paths.
    
- **`zebra` (The Manager):** This program takes the "best paths" calculated by `ospfd` and actually programs them into the system. It manages the router's interfaces (IP addresses, up/down status).
    

### 2. The "Muscle" (Data Plane)

- **Linux Kernel:** The text clarifies that FRR doesn't actually _move_ the packets. Once `zebra` tells the system "send packets for X out of interface Y," the **Linux Kernel** does the heavy lifting of actually forwarding the traffic.
    

### 3. The Setup (Configuration)

- **`conf/` directory:** It explains that when you start the simulation, the routers don't begin empty. They automatically load startup settings from files located in a `conf/` folder. This mimics a real router booting up with a "startup-config."
    

### 4. The Tool You Will Use (Interface)

- **`vtysh`:** Finally, it tells you how to interact with the router. You won't be editing text files or talking to `zebra` directly. You will use `vtysh`, a command-line shell that combines everything into one interface (similar to a Cisco CLI).

![[Pasted image 20260103201051.png]]


### Summary
"We have built a virtual router using Linux and FRR. It runs OSPF (`ospfd`) and a manager (`zebra`). We've already pre-configured it using files in the `conf` folder. To control it and look around, you need to use the `vtysh` command

![[Pasted image 20260103201136.png]]### Question 1.1: Why do the routers need time before we can interact with them? What processes are starting during this time?

The 15-second sleep timer is required to allow the **OSPF Convergence** process to complete. Unlike simple static routing, OSPF is a dynamic Link-State protocol that must "learn" the network before it can route packets.

During this time, the following specific processes occur:

1. **Daemon Initialization:** The `zebra` (kernel manager) and `ospfd` (OSPF protocol) daemons must boot up and load their configuration files.
    
2. **Hello Packet Exchange:** Routers send "Hello" packets to multicast addresses to discover directly connected neighbors (e.g., Router1 discovers Router2 and Router3).
    
3. **Adjacency Formation:** Neighbors transition through several states (Init $\rightarrow$ ExStart $\rightarrow$ Exchange $\rightarrow$ Loading $\rightarrow$ Full) to establish a reliable relationship.
    
4. **LSDB Synchronization:** Routers exchange Link State Advertisements (LSAs) so that every router builds an identical **Link-State Database (LSDB)**—a complete map of the network topology.
    
5. **SPF Calculation:** Once the database is full, each router runs the Dijkstra (Shortest Path First) algorithm to calculate the best route to every destination and installs these routes into the routing table.
![[Pasted image 20260103201327.png]]### Question 1.2: What networks can router1 directly reach? Which networks require routing through other routers?

Based on the "Week 8 lab topology" subnet list, we can categorize the networks relative to **Router1**:

**Directly Connected Networks (Reachable without OSPF):** Router1 is physically connected to these subnets. It knows about them simply because its interfaces are configured with IP addresses in these ranges.

- **10.0.0.0/24:** The LAN containing HomePC, pc1, and pc2.
    
- **10.0.1.0/24:** The link connecting Router1 to Router2.
    
- **10.0.3.0/24:** The link connecting Router1 to Router3.
    

**Remote Networks (Require Routing):** Router1 cannot see these networks directly. It relies on OSPF updates from its neighbors to learn about them.

- **10.0.2.0/24:** Located behind Router2 (contains telnet/ssh hosts).
    
- **10.0.5.0/24:** Located behind Router2 (contains web host).
    
- **10.0.4.0/24:** Located behind Router3 (connects Router3 to Router4).


Based on the topology descriptions and standard OSPF routing behavior (shortest path), here are the answers to your quiz questions.

### Question 1: What is the default gateway IP for host homePC?

- **Answer:** **10.0.0.1**
    
- **Evidence from image:** `HomePC` is connected to `switch1`. `router1` is also connected to `switch1`. The interface on `router1` facing that switch is labeled **10.0.0.1/24** in red. This is the gateway for all PCs on that left-hand network.
    

### Question 2: Path used when host homePC pings host telnet?

- **Answer:** **homePC -> router1 -> router2 -> telnet**
    
- **Evidence from image:**
    
    - **Start:** `HomePC` (10.0.0.2)
        
    - **Hop 1:** `router1` (Gateway 10.0.0.1)
        
    - **Hop 2:** `router1` is connected to `router2` directly via the 10.0.1.0/24 network (specifically, `router1` is 10.0.1.2 and `router2` is 10.0.1.1). This is the direct, shortest path. Going through `router3` adds an extra hop.
        
    - **Hop 3:** `router2` connects to `switch2` where the `telnet` host resides.
        
    - **End:** `telnet` (10.0.2.10)
        

### Question 3: Which subnet connects router1 and router3?

- **Answer:** **10.0.3.0/24**
    
- **Evidence from image:** The line connecting `router1` and `router3` has two IP labels: `10.0.3.2/24` (on the router1 side) and `10.0.3.1/24` (on the router3 side). This confirms the subnet is 10.0.3.0/24.
    

### Question 4: Traceroute path between homePC and telnet?

Based on the IPs in the diagram, the traceroute output will be:

1. **Hop 1 (Gateway):** `10.0.0.1` (Router1's LAN interface)
    
2. **Hop 2 (Next Router):** `10.0.1.1`
    
    - _Correction from previous response:_ Looking closely at the diagram, the interface on **router2** facing router1 is labeled `10.0.1.1/24`. (My previous text guess said 10.0.1.2, but the diagram shows `.1` on the router2 side and `.2` on the router1 side).
        
3. **Hop 3 (Destination):** `10.0.2.10` (The telnet host IP shown in the top right).
    

**Corrected Traceroute Selection:**

- Blank 1: **10.0.0.1**
    
- Blank 2: **10.0.1.1** (This is the specific IP of router2 that router1 talks to)
    
- Blank 3: **10.0.2.10**