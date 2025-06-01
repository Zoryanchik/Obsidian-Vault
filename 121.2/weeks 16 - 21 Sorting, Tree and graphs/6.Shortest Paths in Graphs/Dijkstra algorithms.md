![[Pasted image 20250315170738.png]]![[Pasted image 20250315170836.png]]
![[Pasted image 20250315171335.png]]
1. **Initialize:**
    
    - Create a set of unvisited nodes and set the initial distances to all nodes as **infinity (∞)**, except for the source node, which is set to **0**.
    - Maintain a priority queue (or min-heap) to process nodes in increasing order of distance.
2. **Visit the Nearest Node:**
    
    - Extract the node with the **smallest** distance from the queue.
    - Mark it as visited (processed).
3. **Update Neighboring Nodes:**
    
    - For each unvisited neighbor of the current node, calculate the potential new distance through the current node.
    - If the new distance is smaller than the recorded distance, update it.
4. **Repeat Until All Nodes Are Processed:**
    
    - Continue this process until all nodes have been visited or the shortest path to the target node is found.

## **Algorithm Implement**
![[Pasted image 20250315171524.png]]
Dijkstra’s Algorithm: Example Execution
![[Pasted image 20250315171607.png]]
![[Pasted image 20250315171638.png]]
![[Pasted image 20250315171653.png]]
![[Pasted image 20250315171722.png]]
![[Pasted image 20250315171751.png]]
![[Pasted image 20250315171857.png]]
![[Pasted image 20250315171933.png]]
![[Pasted image 20250315172012.png]]