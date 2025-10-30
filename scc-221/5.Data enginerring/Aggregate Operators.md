![[Pasted image 20251029215359.png]]![[Pasted image 20251029215415.png]]![[Pasted image 20251029215433.png]]![[Pasted image 20251029215444.png]]`DISTINCT` here means "only consider **unique** values" when calculating the average.
![[Pasted image 20251029215711.png]]![[Pasted image 20251029215820.png]]You are right to be confused, as `S2` is not a different table.

**`S2` is just a temporary nickname (an alias) for the `Sailors` table.**

In this query, the `Sailors` table is actually being used twice:

1. **Once in the outer query:** `FROM Sailors S` (Here, its nickname is `S`)
    
2. **Once in the nested query:** `FROM Sailors S2` (Here, its nickname is `S2`![[Pasted image 20251029220032.png]]![[Pasted image 20251029220142.png]]![[Pasted image 20251029220227.png]]