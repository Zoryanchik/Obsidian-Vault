![[Pasted image 20251028191136.png]]![[Pasted image 20251028191431.png]]![[Pasted image 20251028191749.png]]![[Pasted image 20251028191855.png]]![[Pasted image 20251028192000.png]]This is a great observation, and it points to a key concept in database design called **participation constraints**.

The `CANNOT NULL` (which is standard SQL `NOT NULL`) is on the right side due to the **total participation** of the `Bus` entity in the relationship.

| **Feature**      | **Previous Diagram (Right)**           | **This Diagram**                        |
| ---------------- | -------------------------------------- | --------------------------------------- |
| **Relationship** | 1:N (`Teacher`-to-`Bus`)               | 1:N (`Teacher`-to-`Bus`)                |
| **`Bus` Rule**   | A `Bus` _must_ be used by a `Teacher`. | A `Bus` _may_ be used by a `Teacher`.   |
| **`Bus` Symbol** | **Double line** (Total Participation)  | **Single line** (Partial Participation) |
| **Foreign Key**  | `TeacherID_FK` in `Bus` table          | `TeacherID_FK` in `Bus` table           |
| **Null Status**  | **`NOT NULL`**                         | **`NULL` is Allowed**                   |
![[Pasted image 20251028192922.png]]![[Pasted image 20251028193036.png]]![[Pasted image 20251028193354.png]]