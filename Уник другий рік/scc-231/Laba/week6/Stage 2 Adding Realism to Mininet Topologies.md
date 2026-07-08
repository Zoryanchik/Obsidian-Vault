![[Pasted image 20251118000930.png]]![[Pasted image 20251118001233.png]]![[Pasted image 20251118001903.png]]![[Pasted image 20251118003349.png]]![[Pasted image 20251118003601.png]]![[Pasted image 20251118004455.png]]![[Pasted image 20251118004748.png]]![[Pasted image 20251118010016.png]]![[Pasted image 20251118010213.png]]
# Complete Guide to This Network Configuration

Let me explain this from the ground up, covering everything you need to understand.

## What is This?

This is a **network configuration** for Mininet (a network simulator). You're creating 4 computers and teaching them how to communicate with each other through **static routing**.

---

## The Basic Concepts You Need

### 1. **IP Address** (like a phone number)

- Every computer needs an address so others can find it
- Format: `10.0.0.1` (four numbers separated by dots)
- The `/24` part means "the first 3 numbers are the neighborhood, the last number is the house"

### 2. **Network Interface** (like a network cable port)

- `h1-eth0` means "the first ethernet port on host 1"
- Some computers have multiple ports (like h2 and h3), so they can connect to multiple networks

### 3. **Routing** (like GPS directions)s

- When a computer wants to send data somewhere, it needs to know which direction to send it
- **Default route** = "if I don't know where to send it, send it here"
- **Specific route** = "to reach this specific network, send it through this neighbor"

---

## The Network Topology

Here's what you're building:

```
    h1                h2                h3                h4
[10.0.0.2]  ←→  [10.0.0.1]    [192.168.0.1] ←→ [192.168.0.2]    [10.1.0.1] ←→ [10.1.0.2]
                     (h2-eth0)      (h2-eth1)     (h3-eth1)         (h3-eth0)      (h4-eth0)
```

**Three separate networks:**

- **Network A**: 10.0.0.0/24 (connects h1 and h2)
- **Network B**: 192.168.0.0/24 (connects h2 and h3)
- **Network C**: 10.1.0.0/24 (connects h3 and h4)

---

## Breaking Down Every Command

### **Block 1: Delete Old Addresses**

```bash
h1 ip addr del 10.0.0.1/8 dev h1-eth0
h2 ip addr del 10.0.0.2/8 dev h2-eth0
h3 ip addr del 10.0.0.3/8 dev h3-eth0
h4 ip addr del 10.0.0.4/8 dev h4-eth0
```

**What it does:** Mininet automatically assigns addresses when it starts. These commands remove them so you can assign your own custom addresses.

**Why:** You want a specific network design, not the default one.

---

### **Block 2: Assign New IP Addresses**

```bash
h1 ip addr add 10.0.0.2/24 dev h1-eth0
```

- Give h1 the address `10.0.0.2` on its ethernet port
- It's in the `10.0.0.0/24` network

```bash
h2 ip addr add 10.0.0.1/24 dev h2-eth0
h2 ip addr add 192.168.0.1/24 dev h2-eth1
```

- h2 has **TWO** network interfaces (it's acting as a router)
- First interface: `10.0.0.1` (connects to h1)
- Second interface: `192.168.0.1` (connects to h3)

```bash
h3 ip addr add 192.168.0.2/24 dev h3-eth1
h3 ip addr add 10.1.0.1/24 dev h3-eth0
```

- h3 also has **TWO** interfaces (also a router)
- First interface: `192.168.0.2` (connects to h2)
- Second interface: `10.1.0.1` (connects to h4)

```bash
h4 ip addr add 10.1.0.2/24 dev h4-eth0
```

- Give h4 the address `10.1.0.2`
- It's in the `10.1.0.0/24` network

---

### **Block 3: Configure Routing Tables**

This is where you tell each computer how to reach networks it's not directly connected to.

```bash
h1 ip route add default via 10.0.0.1
```

**Translation:** "h1, for ANY destination you don't know about, send the data to 10.0.0.1 (which is h2)"

**Why:** h1 only knows about the 10.0.0.0/24 network. For everything else, it trusts h2 to forward it.

---

```bash
h2 ip route add 10.1.0.0/24 via 192.168.0.2
```

**Translation:** "h2, to reach the 10.1.0.0/24 network, forward data to 192.168.0.2 (which is h3)"

**Why:** h2 doesn't directly connect to the 10.1.0.0/24 network where h4 lives, but h3 does. So h2 forwards traffic destined for that network to h3.

---

```bash
h3 ip route add 10.0.0.0/24 via 192.168.0.1
```

**Translation:** "h3, to reach the 10.0.0.0/24 network, forward data to 192.168.0.1 (which is h2)"

**Why:** h3 doesn't directly connect to the 10.0.0.0/24 network where h1 lives, but h2 does. So h3 forwards traffic destined for that network to h2.

---

```bash
h4 ip route add default via 10.1.0.1
```

**Translation:** "h4, for ANY destination you don't know about, send the data to 10.1.0.1 (which is h3)"

**Why:** h4 only knows about the 10.1.0.0/24 network. For everything else, it trusts h3 to forward it.

---

## How Data Actually Flows

### Example: h1 wants to ping h4

1. **h1 thinks:** "I want to reach 10.1.0.2 (h4). That's not in my local network (10.0.0.0/24), so I'll use my default route and send it to 10.0.0.1 (h2)"
    
2. **h2 receives it and thinks:** "This is going to 10.1.0.2, which is in the 10.1.0.0/24 network. I have a route for that! Send it to 192.168.0.2 (h3)"
    
3. **h3 receives it and thinks:** "This is going to 10.1.0.2. That's in my directly connected network 10.1.0.0/24, so I can deliver it directly to h4"
    
4. **h4 receives the ping!**
    

### Return Path: h4 replies to h1

1. **h4 thinks:** "Reply to 10.0.0.2 (h1). Not in my local network, use default route to 10.1.0.1 (h3)"
    
2. **h3 thinks:** "Going to 10.0.0.2, that's in the 10.0.0.0/24 network. My route says send it to 192.168.0.1 (h2)"
    
3. **h2 thinks:** "Going to 10.0.0.2. That's in my directly connected network 10.0.0.0/24, deliver it directly to h1"
    
4. **h1 receives the reply!**
    

---

## Key Takeaways

- **h1 and h4** are simple hosts with one connection each
- **h2 and h3** are acting as **routers** - they forward traffic between different networks
- **Static routing** means you manually configure every route (as opposed to routers automatically figuring it out)
- Each routing decision is based on the **destination IP address** of the packet
- This creates a **multi-hop network** where data travels through intermediary nodes to reach its destination

This is the foundation of how the internet works, just on a much larger scale!![[Pasted image 20251118011225.png]]
![[Pasted image 20251118010711.png]]![[Pasted image 20251118010723.png]]# Understanding Mininet Network Configuration - A Beginner's Guide

Let me break this down into simple concepts! Think of this like setting up a small office network, but in a virtual environment.

## 🏠 The Big Picture: What Are We Building?

Imagine you have **4 computers** (h1, h2, h3, h4) in two different offices that need to talk to each other:

- **Office 1**: h1 and h2 (connected by switch s1)
- **Office 2**: h3 and h4 (connected by switch s2)
- **Bridge between offices**: h2 and h3 act as routers connecting the two offices

## 🔑 Core Concepts Explained Simply

### 1. **IP Addresses** (Like Home Addresses)

Just like your house has a street address, each computer needs an IP address to receive data.

- `10.0.0.2/24` means:
    - **10.0.0.2** is the specific address
    - **/24** means "I'm in a neighborhood with addresses from 10.0.0.0 to 10.0.0.255"

### 2. **Routers** (Like Post Offices)

- h2 and h3 are special computers that **forward packages** between the two offices
- They use `LinuxRouter` class to gain routing superpowers
- `sysctl net.ipv4.ip_forward=1` turns on the "forwarding" ability

### 3. **Routes** (Like GPS Directions)

When h1 wants to send data to h4, it needs directions:

- **Default Route**: "If I don't know where to send it, send it to h2"
- **Static Route**: "To reach the 10.1.0.0/24 network, go through 192.168.0.1"

## 📋 Let's Walk Through The Code

### **Step 1: Creating Hosts**

python

```python
h1 = self.addHost('h1', ip='10.0.0.2/24', defaultRoute='via 10.0.0.1')
```

**Translation**:

- Create computer h1
- Give it address 10.0.0.2
- Tell it: "When you don't know where to send something, send it to 10.0.0.1 (which is h2)"

python

```python
h2 = self.addHost('h2', ip='10.0.0.1/24', cls=LinuxRouter, 
                   routes=[('10.1.0.0/24', '192.168.0.1')])
```

**Translation**:

- Create h2 as a **router** (not just a computer)
- Give it address 10.0.0.1
- Add a route: "To reach network 10.1.0.0/24, forward through 192.168.0.1 (which is h3)"

### **Step 2: Creating Switches**

python

```python
s1 = self.addSwitch('s1')
```

**Translation**: Create a network switch (like a power strip, but for network cables). Switches connect devices in the same local network.

### **Step 3: Connecting Everything**

python

```python
self.addLink(h1, s1, intfName1='h1-eth0', params1={'ip': '10.0.0.2/24'}, 
             bw=100, delay="30ms", loss=1)
```

**Translation**:

- Connect h1 to switch s1 with a cable (interface h1-eth0)
- This cable can carry 100 Mbps
- It takes 30 milliseconds for data to travel through
- 1% of packets might get lost (simulating real-world imperfections)

## 🛤️ How Data Flows: h1 Pinging h4

Let's trace what happens when h1 sends a ping to h4:

1. **h1 thinks**: "10.1.0.2 is not in my neighborhood (10.0.0.0/24), so I'll use my default route"
2. **h1 sends** → to h2 (10.0.0.1)
3. **h2 thinks**: "I have a route! To reach 10.1.0.0/24, go through 192.168.0.1"
4. **h2 forwards** → to h3 (via 192.168.0.1)
5. **h3 forwards** → to h4 (which is in its local network)
6. **h4 receives** the ping and replies back the same way!

## 🔍 Key Parameters Explained

|Parameter|What It Does|Example|
|---|---|---|
|`ip`|Sets the IP address|`'10.0.0.2/24'`|
|`defaultRoute`|Where to send unknown destinations|`'via 10.0.0.1'`|
|`cls=LinuxRouter`|Makes host act as router|Routes traffic between networks|
|`routes`|Specific directions to networks|`[('10.1.0.0/24', '192.168.0.1')]`|
|`bw`|Bandwidth (speed)|`100` = 100 Mbps|
|`delay`|How long data takes to travel|`'30ms'`|
|`loss`|Packet loss percentage|`1` = 1% loss|

## 🎯 Why This Setup Works

The topology creates **three networks**:

1. **Network 1** (10.0.0.0/24): h1 ↔ s1 ↔ h2
2. **Network 2** (10.1.0.0/24): h3 ↔ s2 ↔ h4
3. **Bridge Network** (192.168.0.0/24): h2 ↔ h3

The routers (h2 and h3) know how to forward traffic between these networks, allowing h1 and h4 to communicate even though they're in completely different networks!

## 🚀 Testing It

When you run `pingall` in Mininet, you're testing if all computers can reach each other. If everything is configured correctly, you'll see 0% packet loss, meaning your virtual network is working perfectly!

---

**Think of it like this**: You've built a miniature internet with two offices, where some computers know how to forward mail between offices so everyone can communicate! 🌐
### Part 1: Adding Network Realism & Task 2: Configuring IP networks and static routes using the Mininet API

```python
from mininet.topo import Topo
from mininet.node import Node


class LinuxRouter(Node):
    def config(self, **params):
        super(LinuxRouter, self).config(**params)
        if 'routes' in params:
            for (ip, gateway) in params['routes']:
                self.cmd('ip route add {} via {}'.format(ip, gateway))
        self.cmd('sysctl net.ipv4.ip_forward=1')

    def terminate(self):
        self.cmd('sysctl net.ipv4.ip_forward=0')
        super(LinuxRouter, self).terminate()


class TutorialTopology(Topo):

    def build(self):
        # add two host to the network
        h1 = self.addHost('h1', ip='10.0.0.2/24', defaultRoute='via 10.0.0.1')
        h2 = self.addHost('h2', ip='10.0.0.1/24', cls=LinuxRouter, routes=[
                          ('10.1.0.0/24', '192.168.0.1')])
        h3 = self.addHost('h3', ip='10.1.0.1/24', cls=LinuxRouter, routes=[
                          ('10.0.0.0/24', '192.168.0.2')])
        h4 = self.addHost('h4', ip='10.1.0.2/24', defaultRoute='via 10.1.0.1')

        # add a switch to the network
        s1 = self.addSwitch('s1')
        s2 = self.addSwitch('s2')

        # add a link between the hosts `h1` and `h2` and the `s1` switch
        self.addLink(h1, s1, intfName1='h1-eth0',
                     params1={'ip': '10.0.0.2/24'}, bw=100, delay="30ms", loss=1)
        self.addLink(h2, s1, intfName1='h2-eth0',
                     params1={'ip': '10.0.0.1/24'}, bw=10, delay="10ms", loss=1)
        self.addLink(h3, s2, intfName1='h3-eth0',
                     params1={'ip': '10.1.0.2/24'}, bw=100, delay="100ms", loss=0)
        self.addLink(h4, s2, intfName1='h4-eth0',
                     params1={'ip': '10.1.0.1/24'}, bw=100, delay="100ms", loss=0)
        self.addLink(h2, h3, intfName1='h2-eth1', intfName2='h3-eth1',
                     params1={'ip': '192.168.0.2/24'}, params2={
                         'ip': '192.168.0.1/24'})


# the topologies accessible to the mn tool's `--topo` flag
# note: if using the Dockerfile, this must be the same as in the Dockerfile
topos = {'tutorialTopology': (lambda: TutorialTopology())}

if __name__ == '__main__':

    # With the code below, you can run the topology directly, using the command `python3 topology.py`
    from mininet.net import Mininet
    from mininet.cli import CLI
    from mininet.log import setLogLevel
    from mininet.nodelib import LinuxBridge
    from mininet.link import TCLink

    setLogLevel('debug')

    topo = TutorialTopology()
    net = Mininet(topo=topo, controller=None,
                  autoSetMacs=True, build=True, switch=LinuxBridge, link=TCLink)
    net.start()
    CLI(net)
    net.stop()
```

python

````python
self.addLink(h2, h3, 
             intfName1='h2-eth1', 
             intfName2='h3-eth1',
             params1={'ip': '192.168.0.2/24'}, 
             params2={'ip': '192.168.0.1/24'})
```

This creates a **direct cable connection** between the two routers (h2 and h3). Think of it as a private highway between two cities.

## 🔌 Breaking Down Each Parameter

### 1. **`h2, h3`** - The Two Endpoints
- We're connecting router h2 to router h3
- This is a **point-to-point** connection (no switch in between!)

### 2. **`intfName1='h2-eth1'`** - h2's Interface Name
- **Interface** = network card/port on the computer
- `eth1` means "Ethernet port #1"
- Remember: h2 already has `h2-eth0` connected to switch s1
- This is h2's **second network card**, so it's `eth1`

**Visual for h2:**
```
h2 (Router)
├── h2-eth0 (IP: 10.0.0.1)    → Connected to s1 (local network)
└── h2-eth1 (IP: 192.168.0.2) → Connected directly to h3 (bridge network)
```

### 3. **`intfName2='h3-eth1'`** - h3's Interface Name
- This is h3's interface on the other end of the cable
- h3 also has two network cards:
  - `h3-eth0` → connects to s2
  - `h3-eth1` → connects to h2

**Visual for h3:**
```
h3 (Router)
├── h3-eth0 (IP: 10.1.0.2)    → Connected to s2 (local network)
└── h3-eth1 (IP: 192.168.0.1) → Connected directly to h2 (bridge network)
```

### 4. **`params1={'ip': '192.168.0.2/24'}`** - h2's IP on This Link
- Sets the IP address for h2's eth1 interface
- **192.168.0.2** is h2's address on the bridge network
- This is different from h2's other IP (10.0.0.1 on eth0)

### 5. **`params2={'ip': '192.168.0.1/24'}`** - h3's IP on This Link
- Sets the IP address for h3's eth1 interface  
- **192.168.0.1** is h3's address on the bridge network
- Different from h3's other IP (10.1.0.1 on eth0)

## 🌉 Why This Link is Special

This creates a **third separate network** (192.168.0.0/24) that exists only between the two routers. It's like a private tunnel connecting two buildings.

### Complete Network View:
```
Network 1 (10.0.0.0/24)          Bridge Network (192.168.0.0/24)          Network 2 (10.1.0.0/24)
┌─────────────────┐              ┌───────────────────┐              ┌─────────────────┐
│                 │              │                   │              │                 │
│  h1             │              │   h2 ←─────→ h3   │              │             h4  │
│  10.0.0.2       │              │   ↑           ↑   │              │       10.1.0.2  │
│      │          │              │   │           │   │              │          │      │
│      │          │              │ eth1        eth1  │              │          │      │
│     s1          │              │ .2            .1  │              │         s2      │
│      │          │              │                   │              │          │      │
│  h2-eth0        │              └───────────────────┘              │      h3-eth0    │
│  10.0.0.1       │                                                 │      10.1.0.1   │
│                 │                                                 │                 │
└─────────────────┘                                                 └─────────────────┘
````

## 🚗 Real-World Analogy

Think of h2 and h3 as **border checkpoint buildings** between two countries:

- **h2-eth0** (10.0.0.1): Door facing Country A (where h1 lives)
- **h2-eth1** (192.168.0.2): Door facing the checkpoint tunnel
- **h3-eth1** (192.168.0.1): Door facing the checkpoint tunnel (other side)
- **h3-eth0** (10.1.0.1): Door facing Country B (where h4 lives)

The **192.168.0.0/24 network** is the tunnel connecting the two checkpoint buildings!

## 📊 Why Two Different IPs Per Router?

Each router needs multiple IP addresses because:

1. **One IP for each network it's connected to**
2. Devices on Network 1 know h2 as **10.0.0.1**
3. h3 knows h2 as **192.168.0.2** (on the bridge)
4. Devices on Network 2 know h3 as **10.1.0.1**
5. h2 knows h3 as **192.168.0.1** (on the bridge)

## 🔄 How Routing Works With This Link

When h1 (10.0.0.2) pings h4 (10.1.0.2):

1. **h1** → sends to default gateway **10.0.0.1** (h2-eth0)
2. **h2** looks at routing table: "10.1.0.0/24 goes via **192.168.0.1**"
3. **h2** forwards packet out **h2-eth1** (192.168.0.2) → to **192.168.0.1**
4. **h3-eth1** (192.168.0.1) receives the packet
5. **h3** sees destination is 10.1.0.2 (local network)
6. **h3** forwards out **h3-eth0** → to **h4**

## ✨ Key Takeaway

This single line creates the **critical bridge** between your two isolated networks. Without it, h1 and h4 could never communicate! The routers use this private 192.168.0.0/24 network to forward traffic between the two separate office networks.

It's like building a hallway between two buildings - each building has its own address system inside, but the hallway has its own address system too! 🏢↔️🏢