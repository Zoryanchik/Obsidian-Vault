![[Pasted image 20260106174335.png]]![[Pasted image 20260106174409.png]]In Data Engineering, arrays within documents often need to be processed, filtered, or expanded to perform calculations.

#### Inspecting and Modifying Arrays (`$project` and `$set`)

You can calculate values across elements in an array (like sum, average, min, max) or reshape the array itself.

**Example:** Calculating the total price of a shopping cart by iterating over an `items` array.

- **`$size`**: Counts elements in the array.
    
- **`$map`**: Iterates over the array (like a `forEach` loop), applying logic to each item.
    
- **`$sum`**: Adds up the results.
    

JavaScript

```java
db.sales.aggregate([
  {
    $project: {
      "customer_id": 1, //simpy includes id
      "num_products": { $size: "$items" }, // Count elements in the 'items' array [cite: 212]
      "total_price": {
        $sum: {
          $map: {          // Iterate over the array [cite: 214]
            input: "$items",
            as: "item",    // Variable for current element [cite: 214]
            in: { $multiply: ["$$item.quantity", "$$item.price"] } // Calculate line cost [cite: 215]
          }
        }
      }
    }
  }
])
```

![[Pasted image 20260106174537.png]]![[Pasted image 20260106175043.png]]![[Pasted image 20260106175249.png]]![[Pasted image 20260106175259.png]]![[Pasted image 20260106175605.png]]![[Pasted image 20260106175637.png]]
сначвало раскладиваем как право потом  групем и симуримем как внищу


![[Pasted image 20260106175824.png]]![[Pasted image 20260106175850.png]]**![[Pasted image 20260106175927.png]]**![[Pasted image 20260106175943.png]]
EXAM QUESTION what type of relationship is this
![[Pasted image 20260106180039.png]]
**### 1. Find the "Foreign Key"

First, identify the field that links the two collections.

- In `db.sales`, you see the field `customer_id: 101`.
    
- This matches the `_id: 101` field in the `db.customers` collection.
    
- This tells you **Sales** are pointing to **Customers**.
    

### 2. Check for "One" (Scalar vs. Array)

Look closely at the `customer_id` field inside a **single** Sale document (e.g., the first one with `_id: 11`).

- **The Code:** `customer_id: 101`.
    
- **The Clue:** The value is a single number (a scalar), **not an array**.
    
- **The Meaning:** Because it is just `101` and not `[101, 102]`, a single sale can only belong to **One** customer.
    

### 3. Check for "Many" (Repetition)

Now, look at the `customer_id` field across **multiple** Sale documents.

- **Document 1 (`_id: 11`):** has `customer_id: 101`.
    
- **Document 4 (`_id: 14`):** _also_ has `customer_id: 101`.
    
- **The Meaning:** Since the ID `101` appears multiple times in the Sales collection, **One** customer can be associated with **Many** sales.**
we want to avoid this one 



![[Pasted image 20260106180610.png]]![[Pasted image 20260106180809.png]]![[Pasted image 20260106180910.png]]### . Joining Collections (`$lookup`)

The `$lookup` stage performs a **Left Outer Join** with another collection in the same database. It adds a new array field containing matching documents from the "foreign" collection.

JavaScript

```java
db.sales.aggregate([
  { 
    $lookup: {
      from: "customers",            // Target collection to join [cite: 738]
      localField: "customer_id",    // Field in 'sales' [cite: 739]
      foreignField: "_id",          // Field in 'customers' to match against [cite: 740]
      as: "customer_details"        // Name of new array field for results [cite: 742]
    }
  },
  // Optional: Convert the single-item array into a simple object
  { $set: { "customer": { $first: "$customer_details" } } } [cite: 770]
])
```
![[Pasted image 20260106181213.png]]![[Pasted image 20260106181415.png]]The `$merge` stage writes the aggregation results to a collection. It must be the last stage and can act as an update or insert (upsert) operation.

![[Pasted image 20260106181750.png]]![[Pasted image 20260106181825.png]]![[Pasted image 20260106182311.png]]