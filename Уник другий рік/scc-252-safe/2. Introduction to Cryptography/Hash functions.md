![[Pasted image 20260118205324.png]]![[Pasted image 20260118205330.png]]![[Pasted image 20260118205352.png]]

- **Preimage Resistance (The "One-Way" Rule):**
    
    - _The Rule:_ If you only have the hash fingerprint ($y$), it should be impossible (computationally difficult) to figure out what the original message ($m$) was4.
        
    - _Analogy:_ You can't un-bake a cake to get the original eggs and flour back.
        
- **Second Preimage Resistance (The "No Copycat" Rule):**
    
    - _The Rule:_ If you have a specific message $m$, you cannot find a _different_ message $m^{\prime}$ that produces the exact same hash5.
        
    - _Why it matters:_ This prevents someone from replacing a legal document with a fake one that looks "valid" to the computer.
        
- **Collision Resistance (The "No Twins" Rule):**
    
    - _The Rule:_ It should be hard to find _any_ two different messages ($m$ and $m^{\prime}$) that accidentally share the same hash6.
        
    - _Note:_ This is the hardest property to achieve. If two different files have the same fingerprint, it's called a **collision**, and the hash function is considered broken.
![[Pasted image 20260118212030.png]]![[Pasted image 20260118212120.png]]