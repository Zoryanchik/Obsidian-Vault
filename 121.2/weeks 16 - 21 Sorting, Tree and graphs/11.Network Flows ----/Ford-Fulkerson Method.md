![[Pasted image 20250420003815.png]]![[Pasted image 20250420004824.png]]The initial flow has  
zero everywhere,
- What is the minimum  
    capacity on these edges?
- This is 0.5.
- - I can route some  
    0.5 units through
- these three edges from  
    the source to the sink.
![[Pasted image 20250420004114.png]]![[Pasted image 20250420005104.png]]![[Pasted image 20250420005132.png]]![[Pasted image 20250420005210.png]]![[Pasted image 20250420005303.png]]![[Pasted image 20250420005425.png]]
- **Start with 0 flow** on all edges.
    
- **Find an augmenting path** — a path from source `s` to sink `t` where **residual capacity** (remaining capacity) is greater than 0 on all edges.
    
- **Augment the flow**:
    
    - Pick the **minimum capacity** `x` along the path.
        
    - For each edge `(u, v)` on the path:
        
        - Increase flow `f(u, v)` by `x`
            
        - Decrease reverse flow `f(v, u)` by `x`
            
- **Repeat** until no more augmenting paths can be found.

![[Pasted image 20250420005739.png]]

