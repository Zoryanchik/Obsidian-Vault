![[Pasted image 20251029205510.png]]![[Pasted image 20251029210438.png]]|Expression|Meaning|
|---|---|
|`S.age`|Displays the sailor’s current age.|
|`age1 = S.age - 5`|Creates a **new attribute (column)** called `age1`, showing the sailor’s age minus 5.|
|`2 * S.age AS age2`|Creates another **new attribute** called `age2`, showing the sailor’s age multiplied by 2.|

![[Pasted image 20251029211104.png]]![[Pasted image 20251029211443.png]]![[Pasted image 20251029212046.png]]Give me the **sailors who reserved red boats**,  
❌ **but NOT** those who also reserved green boats.
**![[Pasted image 20251029212225.png]]**![[Pasted image 20251029212250.png]]![[Pasted image 20251029212339.png]]![[Pasted image 20251029212349.png]]![[Pasted image 20251029212616.png]]In SQL, `INTERSECT` is a set operator that takes the results of two queries and returns **only the rows that appear in both result sets**.
![[Pasted image 20251029213150.png]]