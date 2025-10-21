![[Pasted image 20251022005014.png]]o create this link in a database, you take the primary key of the "one" side (`DName` from `Department`) and add it as a column in the "many" side's table (`StudentsEnrol`). This new column is called a **foreign key**.

So, `DepName` is included in the `StudentsEnrol` SQL table to physically create the `Enrols` link shown in the diagram. It's the "glue" that connects a student record to a department record.
![[Pasted image 20251022005509.png]]![[Pasted image 20251022005526.png]]![[Pasted image 20251022005750.png]]![[Pasted image 20251022010009.png]]