![[Pasted image 20251022005014.png]]o create this link in a database, you take the primary key of the "one" side (`DName` from `Department`) and add it as a column in the "many" side's table (`StudentsEnrol`). This new column is called a **foreign key**.

So, `DepName` is included in the `StudentsEnrol` SQL table to physically create the `Enrols` link shown in the diagram. It's the "glue" that connects a student record to a department record.
![[Pasted image 20251022005509.png]]![[Pasted image 20251022005526.png]]![[Pasted image 20251022005750.png]]![[Pasted image 20251022010009.png]]![[Pasted image 20251022010728.png]]That's a great question. The relational schema shown in the slide **does have a foreign key**, but the way the first two tables (`Player` and `Character`) are combined might be causing the confusion.

The foreign key exists in the `Inventory_OWN_Character` table.

---

### ## Where the Foreign Key Is

Let's look at the second table definition:

`Inventory_OWN_Character(item_type:INT, price:INT, wearable:BOOLEAN, charactername:TEXT, **FOREIGN KEY: charactername REFERENCING Player_OWN_Character**, ON DELETE CASCADE, ...)`

This line explicitly creates a **foreign key**.

- **What it does:** It links the `charactername` in the `Inventory` table to the `charactername` in the `Player_OWN_Character` table.
    
- **Why it's there:** This ensures that an inventory item can only be owned by a character that actually exists in the database. It enforces the `OWN` relationship between `Character` and `Inventory`.
    

---

### ## Why the First Table Doesn't Have a Foreign Key

This is the likely source of your question. You might expect a foreign key to link `Player` and `Character`, but there isn't one because the designer chose to **merge the Player and Character tables into one**.

Look at the relationship in the diagram: It's a **one-to-many** relationship (`1` to `N`) between `Player` and `Character`.

A common way to implement this is to create two tables:

1. A `Player` table.
    
2. A `Character` table with a foreign key column (e.g., `player_id`) that points to the `Player` table.
    

However, the solution in the slide uses a different method. It takes all the attributes of the `Player` (`ID`, `name`, `email`) and adds them directly into the `Character` table, creating one big table called `Player_OWN_Character`.

**Because they are merged into a single table, there is no need for a foreign key to link them—the link is implicit in the table's structure.**

This design choice has a major drawback: **data redundancy**. If one player has five characters, that player's `ID`, `name`, and `email` will be repeated five times in the table, which is generally not ideal in database design.