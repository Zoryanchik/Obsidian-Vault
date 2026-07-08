![[Pasted image 20250304172322.png]]
`private Node root;`

- This is the **root node** of the binary search tree, where the tree starts.
-
Each node contains:

- **key**: Used for ordering nodes (like integers or strings).
- **value**: The data stored at this node.
- **leftChild**: Pointer to the **left subtree**.
- **rightChild**: Pointer to the **right subtree**![[Pasted image 20250304172717.png]]
![[Pasted image 20250304172920.png]]

`int cmp = key.compareTo(x.key);`

What happens here?

|Code|What it Means|
|---|---|
|`key`|Your **target** (9 in this case)|
|`x.key`|Current node's key (like 7, 8, 9 during the search)|
|`compareTo()`|Compares both keys|
![[Pasted image 20250304173520.png]]
