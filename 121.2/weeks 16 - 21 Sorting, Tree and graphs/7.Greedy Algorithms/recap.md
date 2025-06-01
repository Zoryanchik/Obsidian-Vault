
![[Pasted image 20250315182851.png]]on^2
![[Pasted image 20250315183026.png]]
its not aa binary search tree
![[Pasted image 20250315183642.png]]
no
      8
     / \
    3   10
    / \    \
 n  //1   6    14
     / \   /
    4   7 13
    this is
    ![[Pasted image 20250315183921.png]]
    no
    ![[Pasted image 20250315184029.png]]
    no 
    **if every vertex is reachable from every other vertex**.
    ![[Pasted image 20250315184359.png]]
    Yes! If the diameter of the graph is **3**, that means the longest shortest path between any two nodes in the graph is 3. This means that for the most distant pair of nodes, the shortest path connecting them consists of three edges.
    The **diameter** of a graph is defined as the **longest shortest path** between any two nodes. That means we:

1. Calculate the shortest path between every pair of nodes.
2. Identify the longest among these shortest paths.
3. That longest shortest path is the **diameter** of the graph.
![[Pasted image 20250315184803.png]]
9