![[Pasted image 20251118000930.png]]![[Pasted image 20251118001233.png]]![[Pasted image 20251118001903.png]]![[Pasted image 20251118003349.png]]![[Pasted image 20251118003601.png]]![[Pasted image 20251118004455.png]]![[Pasted image 20251118004748.png]]![[Pasted image 20251118010016.png]]![[Pasted image 20251118010213.png]]![[Pasted image 20251118011225.png]]
# ✅ **1. Delete the Default Mininet IP Addresses**

`h1 ip addr del 10.0.0.1/8 dev h1-eth0 h2 ip addr del 10.0.0.2/8 dev h2-eth0 h3 ip addr del 10.0.0.3/8 dev h3-eth0 h4 ip addr del 10.0.0.4/8 dev h4-eth0`

Mininet assigns IPs automatically with a **/8 subnet**, which would put _all_ hosts in the same network.  
But you _want three separate networks_, so you **delete** the defaults.

---

# ✅ **2. Assign New IP Addresses (3 networks)**

### **Network A: h1 ↔ h2**

`h1 ip addr add 10.0.0.2/24 dev h1-eth0 h2 ip addr add 10.0.0.1/24 dev h2-eth0`

This link is now **10.0.0.0/24**.

- h1 = 10.0.0.2
    
- h2 = 10.0.0.1 (gateway for h1)
    

---

### **Network B: h2 ↔ h3**

`h2 ip addr add 192.168.0.1/24 dev h2-eth1 h3 ip addr add 192.168.0.2/24 dev h3-eth1`

This link is **192.168.0.0/24**.

- h2 = 192.168.0.1
    
- h3 = 192.168.0.2
    

---

### **Network C: h3 ↔ h4**

`h3 ip addr add 10.1.0.1/24 dev h3-eth0 h4 ip addr add 10.1.0.2/24 dev h4-eth0`

This link is **10.1.0.0/24**.

- h3 = 10.1.0.1
    
- h4 = 10.1.0.2 (gateway for h4)
    

---

# ✅ **3. Add Routing Rules (Static Routes)**

## **h1 needs to reach everything through h2**

`h1 ip route add default via 10.0.0.1`

Meaning:  
“Anything not in my local network → send to h2”

---

## **h2 is a router with 2 interfaces**

It knows:

- 10.0.0.0/24 directly
    
- 192.168.0.0/24 directly
    

But NOT the network behind h3 (10.1.0.0/24).  
So we add:

`h2 ip route add 10.1.0.0/24 via 192.168.0.2`

Meaning:  
“To reach h4’s network, send to h3.”

---

## **h3 is also a router**

It knows:

- 192.168.0.0/24 directly
    
- 10.1.0.0/24 directly
    

But NOT h1’s network (10.0.0.0/24).  
So we add:

`h3 ip route add 10.0.0.0/24 via 192.168.0.1`

Meaning:  
“To reach h1, send packets to h2.”

---

## **h4 needs its gateway set to h3**

`h4 ip route add default via 10.1.0.1`

Meaning:  
“All non-local traffic goes toward h3.”

---

# 🔥 Final Result (What You Achieved)

### ✔ h1 → h2 → h3 → h4 works

### ✔ h4 → h3 → h2 → h1 works

### ✔ All hosts can ping each other

### ✔ Your topology now has **three real subnets**, and static routes forward packets between them

### ✔ h2 and h3 behave like routers![[Pasted image 20251118010711.png]]![[Pasted image 20251118010723.png]]