![[Pasted image 20251114195327.png]]![[Pasted image 20251114195545.png]]As input λ approaches output limit R/2 per flow:

- Throughput caps at R/2
    
- Delay grows endlessly
![[Pasted image 20251114195901.png]]![[Pasted image 20251114200247.png]]![[Pasted image 20251114200348.png]]![[Pasted image 20251114200513.png]]![[Pasted image 20251114200614.png]]![[Pasted image 20251114200740.png]]![[Pasted image 20251114201104.png]]- Upstream traffic is wasted if packets are eventually dropped downstream.
    t means you've used your limited upload bandwidth to send a piece of data, but it never reached its destination, so the effort was completely wasted.
- As load increases, flows interfere.
    
- Some flows get zero throughput when queue collapses.
![[Pasted image 20251114201349.png]]