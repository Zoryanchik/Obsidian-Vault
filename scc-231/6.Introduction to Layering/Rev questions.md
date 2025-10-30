![[Pasted image 20251030183919.png]]Here are the explanations for the revision questions on the slide.

### 1. End-to-End Packet Delay
- **$T_{\text{trans}}$ (Source to Router):** The time to transmit the packet from the source to the router.
    
- **$T_{\text{proc}}$ (At Router):** The processing delay at the router.
    
- **$T_{\text{trans}}$ (Router to Destination):** The time to transmit the packet from the router to the destination.
The total end-to-end delay is the sum of the time it takes to get the packet from the source to the switch _plus_ the time it takes to get it from the switch to the destination.

Since the switch uses **store-and-forward**, it must receive the _entire_ packet ($L$ bits) before it can begin sending it.

1. **Delay (Source to Switch):** The time to transmit $L$ bits over a link with rate $R_1$ is $\frac{L}{R_1}$.
    
2. **Delay (Switch to Destination):** After the switch has received the whole packet, it transmits the $L$ bits over a link with rate $R_2$. This takes $\frac{L}{R_2}$.
    

The total delay is the sum of these two transmission delays.

**Total End-to-End Delay = $\frac{L}{R_1} + \frac{L}{R_2}$**

---

### 2. Users with Circuit Switching

With **circuit switching**, a dedicated, fixed amount of bandwidth must be reserved for each user for the _entire duration_ of their connection, whether they are actively using it or not.

- **Total Link Capacity:** 1 Mbps (or 1,000 kbps)
    
- **Required per User:** 100 kbps
    

The 5% "active" time is irrelevant for circuit switching, as the 100 kbps circuit is reserved regardless.

The calculation is:

$$\frac{\text{Total Capacity}}{\text{Capacity per User}} = \frac{1000 \text{ kbps}}{100 \text{ kbps}} = 10 \text{ users}$$

**Answer:** A 1 Mbps link can support **10 users** using circuit switching.

---

### 3. Circuit vs. Packet Switching for Telephony

Here’s a comparison of the two approaches for a telephony service:

#### 📞 Circuit Switching

- **Benefits:**
    
    - **High User Satisfaction (Quality):** Once a call is connected, the quality is guaranteed. You have a dedicated circuit, so there is no delay, jitter (variation in delay), or packet loss due to congestion.
        
- **Drawbacks:**
    
    - **Cost & Efficiency:** Highly inefficient. Bandwidth is reserved even when users are silent (which is most of the time in a conversation). This means the 1 Mbps link is mostly idle, making it a very costly way to support users.
        
    - **User Satisfaction (Connection):** It can lead to **call blocking**. If all 10 circuits are in use, the 11th user gets a "busy signal" and cannot make a call.
        

#### 🖥️ Packet Switching (e.g., VoIP)

- **Benefits:**
    
    - **Cost & Efficiency:** Far more efficient and less costly. It uses **statistical multiplexing**. The link is shared, and packets (bits of voice) are only sent when a user is actively speaking. This allows _many more_ than 10 users to share the link, as it's unlikely they will all speak at the exact same time.
        
    - **User Satisfaction (Connection):** No call blocking. A user can always _start_ a call (though the quality may suffer if the network is too busy).
        
- **Drawbacks:**
    
    - **User Satisfaction (Quality):** Variable quality. Because the link is shared, packets are subject to:
        
        - **Delay (Latency):** Can make conversation unnatural.
            
        - **Jitter:** Packets arrive at irregular intervals, making audio choppy.
            
        - Packet Loss: If the network is too congested, packets may be dropped, causing audio cutouts.
            
            This makes it more complex to deliver high-quality, real-time voice service compared to the "guaranteed" nature of circuit switching.