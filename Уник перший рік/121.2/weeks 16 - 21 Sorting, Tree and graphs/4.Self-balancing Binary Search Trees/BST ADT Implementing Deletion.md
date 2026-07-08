![[Pasted image 20250304174759.png]]
![[Pasted image 20250304174830.png]]
![[Pasted image 20250304175058.png]]
![[Pasted image 20250304175648.png]]
       20
      /  \
    10    30
   /  \
  5   15
     /
   12

![[Pasted image 20250304175215.png]]
private Node successor(Node x) {
    if (x == null || x.rightChild == null) return null; // 1️⃣
    else {
        x = x.rightChild;        // 2️⃣
        while (x.leftChild != null) {   // 3️⃣
            x = x.leftChild;
        }
        return x;               // 4️⃣
    }
}
![[Pasted image 20250304175341.png]]
![[Pasted image 20250304175423.png]]
![[Pasted image 20250304175451.png]]
