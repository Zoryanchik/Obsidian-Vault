/*
Big O T(n) e O(f(n)) T(n)<=M*fn n >= 0
Big omega. Below .Tn >= M *Fn   for n >= n0
Big sigma is bounded from above and below  M1 *fn <= tn <= M2fn
![[Pasted image 20250206200939.png]]
Linear search Best 01 0logn on
              Average on onlogn on2
              worst on onlogn on2

Linear search on Best 01 0logn on
              Average on onlogn on2
              worst on onlogn on2              

Linear search om 1 Best 01
              Average on onlogn o1
              worst on onlogn o1

Linear search sn Best  01
              Average on
              worst on

Tree = nonlinear abstract data type, stores elemnts hierarchily 
Tree = nodes connected by edges
Root childre3n leaf
Descenfants vnuki
Ancestor ded vse po verhy

Height of a node = number pf nodes on longest path
Depth of a node =number of nodes to root
Diametr of tree =number of nodes vsex znizy

edges = nodes - 1
Balance tree = for any node, the heights of its child subtrees differ by less 1

Preorder = Root(top), left,(to the end), right
Postorder = Left(bottom), Right, Root
Inorder = Left, root, right
levelorder = root, all subtree from left

Graph = set of nodes and edges
Subgraph S of some graph G is a subset of the nodes and edges of G
subrgaph induced all the edges
MST = spanning tree with minimal totl sum of edge weights
Complementary graph =Same set of nodes but with completiy different edges
Density = of a graph is a measure btw0 and 1 how heavily connected
2E pos n(n-1)
Direct is strong if we can reach any node from any other

Graph adr mem n2 wc node n2 removing node adding or rwmoving 0(1 )

DFS
1)Start at the source,and visit a neigbor (visited)
2)From neigbour to the other one
3)Repeat until you hit an already visited
4)Backtrrack and repeat
In stack ex 5 4 3 2
BFS
Same but and then traversal edge (5, 3)
Queue

Dijkstra algorithms
Create a set of unvisited nodes and set the initial distances to all nodes as **infinity (∞)**, except for the source node, which is set to **0**.
Extract the node with the **smallest** distance from the queue
For each unvisited neighbor of the current node, calculate the potential new distance through the current node.
continiue till the end
on2 or m nlogn if all pos

A* dv + hv actual cost and estimated

BellmanFord start from any
 Works by **relaxing all edges** multiple times.
- Updates the shortest distances by checking each edge **V-1 times**
 Can **detect negative-weight cycles** by performing one more iteration.
- **Use case**: Works well when the graph has **negative weights**.

Diametr  the longest shortest path between any two nodes in the graph

Greedy algor: start at source and go through each stage, looking at on ethat is closest

Dynamic Programming (DP) is a method for **solving complex problems by breaking them down into smaller subproblems

*/
