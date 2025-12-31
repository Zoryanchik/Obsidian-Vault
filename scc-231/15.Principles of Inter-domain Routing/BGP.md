![[Pasted image 20251230230342.png]]![[Pasted image 20251230230449.png]]![[Pasted image 20251230230512.png]]we promise to froward the traffic to x 
![[Pasted image 20251230230636.png]]
![[Pasted image 20251230230653.png]]![[Pasted image 20251230230933.png]]![[Pasted image 20251230231114.png]]![[Pasted image 20251230231301.png]]The final slide shows how a router actually decides where to send a packet using **BGP** (Border Gateway Protocol).

1. **External Info:** Router **1c** (a gateway) learns from another network (AS3) how to reach destination **X**.
    
2. **Internal Info:** Router **1c** tells its friends inside its own network (1a, 1b, 1d) that it is the "exit door" for X.
    
3. **The Decision:** Router **1a** looks at its table. It knows from its internal map (OSPF) that to get to **1c**, it must use **Interface 2**. Therefore, to get to **X**, it also uses **Interface 2**.
- 1. Go through router **1b** (Interface 1).
        
    2. Go through router **1d** (Interface 2).
        
- In this specific diagram, the path through **1d** is the **shortest/lowest cost path**.
    
- Therefore, the router's internal table says: _"To get to 1c, use Interface 2"_.

![[Pasted image 20251230231555.png]]![[Pasted image 20251230231706.png]]![[Pasted image 20251230231718.png]]![[Pasted image 20251230231755.png]]![[Pasted image 20251230232040.png]]![[Pasted image 20251230232130.png]]![[Pasted image 20251230232238.png]]![[Pasted image 20251230232249.png]]