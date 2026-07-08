![[Pasted image 20251114201841.png]]![[Pasted image 20251114202043.png]]![[Pasted image 20251114202530.png]]![[Pasted image 20251114202649.png]]Based on that slide, **"inferred" means to deduce or figure out indirectly.**

The network doesn't send a _direct_ or _explicit_ message back to your computer saying, "Hey, I'm congested! Slow down!"
![[Pasted image 20251114203029.png]]![[Pasted image 20251114203224.png]]# **8. AIMD (Additive Increase, Multiplicative Decrease)**

### **Additive Increase (AI)**

- Increase cwnd by 1 MSS every RTT
    
- Slowly probes for available bandwidth
    

### **Multiplicative Decrease (MD)**

- If congestion (loss) occurs:
    
    - On **triple dup ACK (Reno)**: cwnd = cwnd / 2
        
    - On **timeout (Tahoe)**: cwnd = 1 MSS
        

Results in **sawtooth pattern**.
![[Pasted image 20251114203517.png]]![[Pasted image 20251114203809.png]]![[Pasted image 20251114203854.png]]![[Pasted image 20251114204108.png]]![[Pasted image 20251114204204.png]]![[Pasted image 20251114204214.png]]Motivation:

- Reno’s linear increase is too slow for high-speed networks.
    

Key ideas:

- Let Wmax = window size when loss occurred.
    
- After reducing cwnd, ramp back to Wmax quickly, then slow down near Wmax.
    
- CUBIC uses a **cubic function** of time since last loss.
    

Properties:

- Default in Linux and many servers (2006–2024).
    
- Better high-throughput performance than Reno.