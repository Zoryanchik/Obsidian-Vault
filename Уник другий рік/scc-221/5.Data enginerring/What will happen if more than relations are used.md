![[Pasted image 20251029204331.png]]![[Pasted image 20251029204343.png]]- **Combine Everything:** First, create a giant, temporary table by combining every single row from all tables listed in the `FROM` clause (a "cross-product").
    
- **Filter:** Go through that giant table and throw away every row that doesn't match your `WHERE` conditions.
    
- **Project:** From the rows that are left, throw away all the columns you _didn't_ ask for in the `SELECT` list.
    
- **Remove Duplicates:** If you used `DISTINCT`, clean up the final result by deleting any identical rows.
- 
![[Pasted image 20251029205622.png]]