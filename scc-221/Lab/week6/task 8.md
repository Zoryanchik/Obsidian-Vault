![[Pasted image 20251116002403.png]]![[Pasted image 20251116002717.png]]![[Pasted image 20251116002733.png]]![[Pasted image 20251116002746.png]]![[Pasted image 20251116002824.png]]![[Pasted image 20251116002858.png]]On Data Item A:
    
T3 reads A: `T3: ...R(A)...
        
 _Later_, T1 writes A: `T1: ...W(A)`
        
 This is a Read-Write conflict. Since T3 comes first, we draw an arrow: **T3 $\rightarrow$ T1**
        
- **On Data Item B:**
    
    - T2 reads B: `T2: ...R(B)...`
        
    - _Later_, T3 writes B: `T3: ...W(B)`
        
    - This is a Read-Write conflict. Since T2 comes first, we draw an arrow: **T2 $\rightarrow$ T3**
        
    - (There is also a Write-Write conflict: T2's W(B) comes before T3's W(B), which _also_ gives the arrow **T2 $\rightarrow$ T3**).![[Pasted image 20251116002906.png]]