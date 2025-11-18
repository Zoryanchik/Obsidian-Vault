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
![[Pasted image 20251118010711.png]]![[Pasted image 20251118010723.png]]