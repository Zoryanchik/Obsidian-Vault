![[Pasted image 20260106010438.png]]![[Pasted image 20260106010454.png]]![[Pasted image 20260106010520.png]]![[Pasted image 20260106010535.png]]![[Pasted image 20260106010602.png]]![[Pasted image 20260106010919.png]]![[Pasted image 20260106010937.png]]![[Pasted image 20260106010951.png]]![[Pasted image 20260106011018.png]]![[Pasted image 20260106011047.png]]

```
{ $group: { _id: "$product_name", // "What to group by" total_revenue: { // "Output name" $sum: "$price" // "Accumulator" : "Expression" (Performed on price) } } }
```


![[Pasted image 20260106011236.png]]![[Pasted image 20260106011327.png]]
![[Pasted image 20260106011349.png]]![[Pasted image 20260106011425.png]]
![[Pasted image 20260106011525.png]]### 2. The Code

The code in the middle is the simplest version of the `$group` command you can write:

JavaScript

```
{ $group: { "_id": "$product" } }
```

It tells MongoDB: "Look at the `product` field. Every time you see a **new** product name, make a 'bucket' for it. If you see a name you already have a bucket for (like another 'A'), just toss it in there." bc of id


![[Pasted image 20260106011928.png]]#### 1. `_id: "$product"`

This is the **Group By** command.

- It tells MongoDB: "Sort all 8 documents into piles based on their Product Name."
    
- Result: You get three piles: A, B, and C.
    

#### 2. `"sales": { $sum: 1 }`

This counts the **Number of Transactions**.

- **Logic:** "Every time you throw a receipt into a pile, add **1** to the counter."
    
- **Real-world meaning:** How many times did customers come to the register?
    
    - _Example:_ Product 'C' appears on 2 distinct receipts, so `sales` is **2**.
        

#### 3. `"sold": { $sum: "$quantity" }`

This sums up the **Total Units Sold**.

- **Logic:** "Look at the `quantity` field on the receipt and add that number to the running total."
    
- **Real-world meaning:** How many physical items left the inventory?
    
    - _Example:_ Product 'C' had quantities of 10 and 15. The total `sold` is **25**.
        

#### 4. `"revenue": { $sum: { $multiply: ["$quantity", "$price"] } }`

This calculates the **Total Money Made**.

- **Logic:** This is a two-step math problem:
    
    1. **First ($multiply):** For _each_ individual receipt, multiply `quantity` $\times$ `price` (e.g., 10 items $\times$ $20 = $200).
        
    2. **Second ($sum):** Add those results together for the whole group.
        
- **Real-world meaning:** What was the total revenue for this product?
    
    - _Example for 'C':_
        
        - Sale 1: $10 \times 20 = 200$
            
        - Sale 2: $15 \times 20 = 300$
            
        - **Total Revenue:** $200 + 300 = \mathbf{500}$.

![[Pasted image 20260106012250.png]]
![[Pasted image 20260106012333.png]]![[Pasted image 20260106012506.png]]![[Pasted image 20260106012801.png]]