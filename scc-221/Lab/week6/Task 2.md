![[Pasted image 20251116000301.png]]![[Pasted image 20251116000347.png]]![[Pasted image 20251116000628.png]]This ERD states that **every Pal has exactly one set of stats, and each set of stats belongs to exactly one Pal.**

The designer likely split the information into two tables for organization:

- `Pals_basic` stores the Pal's general information (like name, key, and wiki links).
    
- `Pal_stats` stores all of its detailed gameplay statistics (like HP, attack, speed, etc.).
![[Pasted image 20251116001400.png]]![[Pasted image 20251116001410.png]]![[Pasted image 20251116001543.png]]![[Pasted image 20251116001551.png]]