![[Pasted image 20251028191136.png]]![[Pasted image 20251028191431.png]]![[Pasted image 20251028191749.png]]![[Pasted image 20251028191855.png]]![[Pasted image 20251028192000.png]]This is a great observation, and it points to a key concept in database design called **participation constraints**.

The `CANNOT NULL` (which is standard SQL `NOT NULL`) is on the right side due to the **total participation** of the `Bus` entity in the relationship.

| **Feature**      | **Previous Diagram (Right)**           | **This Diagram**                        |
| ---------------- | -------------------------------------- | --------------------------------------- |
| **Relationship** | 1:N (`Teacher`-to-`Bus`)               | 1:N (`Teacher`-to-`Bus`)                |
| **`Bus` Rule**   | A `Bus` _must_ be used by a `Teacher`. | A `Bus` _may_ be used by a `Teacher`.   |
| **`Bus` Symbol** | **Double line** (Total Participation)  | **Single line** (Partial Participation) |
| **Foreign Key**  | `TeacherID_FK` in `Bus` table          | `TeacherID_FK` in `Bus` table           |
| **Null Status**  | **`NOT NULL`**                         | **`NULL` is Allowed**                   |
![[Pasted image 20251028192922.png]]![[Pasted image 20251028193036.png]]![[Pasted image 20251028193354.png]]****
![[Pasted image 20251028194220.png]]![[Pasted image 20251028194439.png]]2.2)

CK{{ID},{Weight}} 
PA {ID,Weight}
NPA {TYPE, SALARY, ADDRESS}

A->T (T->A)

2.3) IN 1NF, IN 2NF, Not in 3NF so the table is in 2NF.
![[Pasted image 20251028195608.png]]
2.4) R1 (ID (PK), TYPE, SALARY,Weight )
     R2 (Type (PK), ADDRESS)  (T->A)
	 
![[Pasted image 20251028195618.png]]![[Pasted image 20251028195948.png]]![[Pasted image 20251028200458.png]]![[Pasted image 20251028200750.png]]![[Pasted image 20251028200858.png]
![[Pasted image 20251028201857.png]
![[Pasted image 20251028202148.png]]![[Pasted image 20251028202344.png]]![[Pasted image 20251028202412.png]]![[Pasted image 20251028204308.png]]![[Pasted image 20251028204540.png]]![[Pasted image 20251028204706.png]]![[Pasted image 20251028205021.png]]![[Pasted image 20251028205211.png]]![[Pasted image 20251028205331.png]]![[Pasted image 20251028205546.png]]
For _any_ functional dependency in the table (like $X \to Y$), the left side ($X$) **must be a superkey**.



![[Pasted image 20251028210048.png]]


3.4) 
a) PA {Weapon, Damage} 
NPA {AmmoType, MaximumAmmo, FireMode,RateofFire, MuzzleVelocity, MaximumRange}

Weapon-> Everything
Damage->Everything
AmmoType->MaximumAmmo,FireMode

b) CK={{Weapon}, {Damage}} 
in 1NF, in 2NF answer is 2NF

c) R1(Weapon,Damage,AmmoType,RateofFire, MuzzleVelocity, MaximumRange)
   R2(AmmoType (PK),MaximumAmmo,FireMode)


   
3.5)
a)
PA {raceID, raceName} NPA {description,iconID,shortDescription}

raceID->Everything
raceName->Everyting
Description->iconID,shortDescription
shortDescription->iconID

b) CK = {{raceID}, {raceName}}

2NF

c) 
R1(raceID,raceName,Description) 
R2(shortDescription,iconID)
R3(Description,shortDescription)
  

