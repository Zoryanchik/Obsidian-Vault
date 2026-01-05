![[Pasted image 20260106005421.png]]#### Query 1: The "Missing Field" Fail

`db.users.find({"name" : {"last" : "Doe"}})`

- **Result:** **No match**.
    
- **Why?** MongoDB is looking for a `name` object that contains **only** the field `last`. Since both actual users also have a `first` name field inside the `name` object, they do not match.
    

#### Query 2: The Successful Exact Match

`db.users.find({"name" : {"first": "Jay", "last" : "Doe"}})`

- **Result:** **Matches only left document**.
    
- **Why?**
    
    - **Left Doc:** Matches perfectly. It has `first: "Jay"` and `last: "Doe"` in that exact order.
        
    - **Right Doc:** Fails because the right document has an extra field (`"middle": "Alex"`). The query didn't include it, so it's not an exact match.
        

#### Query 3: The "Wrong Order" Fail

`db.users.find({"name" : {"last" : "Doe", "first": "Jay"}})`

- **Result:** **No match**.
    
- **Why?** Even though the left document has both "Doe" and "Jay", the query lists them in the **wrong order** (Last then First). In embedded document matching, order matters.

If you try to match a whole object (like `name: {...}`), you must get every single field right, and in the right order.


![[Pasted image 20260106005650.png]]
![[Pasted image 20260106005817.png]]

![[Pasted image 20260106005753.png]]![[Pasted image 20260106005937.png]]