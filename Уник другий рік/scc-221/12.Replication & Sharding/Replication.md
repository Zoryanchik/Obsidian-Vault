![[Pasted image 20260106183135.png]]Replication ensures that your data is safe even if a server fails. It works by creating copies of your data across multiple servers .

#### **The Architecture: Replica Sets**

A **Replica Set** is a group of MongoDB servers that hold the same data.

- **Primary Node (1):** The "Boss". It is the **only** node that accepts **Write** operations. It also handles reads by default .
    
- **Secondary Nodes (N):** The "Backups". They constantly copy data from the Primary to stay up-to-date.

**![[Pasted image 20260106183209.png]]**
![[Pasted image 20260106183314.png]]#### **How it Works**

1. **Oplog (Operations Log):** When you write to the Primary, it records the operation in a "circular buffer" log called the `oplog`.
    
2. **Syncing:** Secondary nodes watch this log and apply the same operations to themselves to match the Primary.
    
3. **Heartbeats:** Every node sends a "ping" (heartbeat) to every other node every 2 seconds to check if they are alive.

![[Pasted image 20260106183435.png]]![[Pasted image 20260106183506.png]]![[Pasted image 20260106183550.png]]![[Pasted image 20260106183612.png]]![[Pasted image 20260106183705.png]]![[Pasted image 20260106183822.png]]![[Pasted image 20260106183842.png]]