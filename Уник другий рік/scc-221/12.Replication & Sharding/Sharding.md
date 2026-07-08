![[Pasted image 20260106183923.png]]![[Pasted image 20260106184002.png]]### 2. Sharding (Horizontal Scaling)

Sharding is used when you have too much data for one machine to handle. It splits the data across multiple machines .

#### **The Architecture**

1. **Shards:** The actual storage units. Each shard holds a _subset_ of the data. (In production, each shard is actually a Replica Set for safety) .
    
2. **Config Servers:** They store the "map" (metadata). They know which shard holds which part of the data .
    
3. **Router (`mongos`):** The traffic cop. Your application connects to this. It looks at the Config Server's map and routes your query to the correct Shard(s) .
    
![[Pasted image 20260106184211.png]]
#### **Shard Keys**

To split data, you must choose a **Shard Key** (a field in your document). MongoDB breaks data into "Chunks" based on this key .

- **Range-Based:** Groups similar values together (e.g., IDs 1-100). Good for range queries, but can cause "hotspots" if everyone writes to the latest date/ID.
    
- **Hash-Based:** Randomly distributes data using a hash of the key. Good for even distribution, but bad for range queries.
    

#### **The Balancer**

This is a background process that ensures no single shard gets too full.

- **Splitter:** If a chunk gets too big, it splits it into two.
    
- **Balancer:** If one shard has more chunks than others, it automatically moves chunks to emptier shards to keep the load even.

![[Pasted image 20260106184259.png]]![[Pasted image 20260106184409.png]]![[Pasted image 20260106184542.png]]### 1. What is the Routing Table?

The routing table is a metadata file that maps specific data ranges to specific shards.

- It tracks **Shard Key Ranges** (e.g., "Users A-F go to Shard 1").
    
- It tells the system exactly which shard is responsible for holding a specific piece of data.
    
- This allows the system to balance the load efficiently.

![[Pasted image 20260106184845.png]]![[Pasted image 20260106184957.png]]![[Pasted image 20260106185018.png]]![[Pasted image 20260106185030.png]]