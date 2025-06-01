![[Pasted image 20250419193017.png]]![[Pasted image 20250419192924.png]]![[Pasted image 20250419193325.png]]![[Pasted image 20250419193419.png]]
```
public class BST<Key extends Comparable<Key>,Value>{

    private Node root;

    private class Node{

        private Key key;

        private Value value;

        private Node leftChild, rightChild;

        private int size; //number of nodes in subtree

        public Node(Key key, Value value, int size){

            this.key = key;

            this.value = value;

            this.size = size;

        }

    }
```
```
    public int size() {

        return size(root);

    }

    // return number of key-value pairs in BST rooted at x

    private int size(Node x) {

        if (x == null) return 0;

        else return x.size;

    }
```
```
public int rank(Key key){

    return rank(root, key);

}

    //Returns number of keys strictly smaller than input key

    // If key is in BST, it is the (rank+1) key in sorted order.  
private int rank(Node x, Key key){

    if (x == null) return 0;

    int cmp = key.compareTo(x.key);

    if (cmp < 0) return rank(x.leftChild, key);

    else if (cmp > 0)

  return 1 + size(x.leftChild) + rank(x.rightChild, key);

    else return size(x.leftChild);

}
```
```  
public int rangeCount(Key low, Key high){

        if (find(high) != null) return rank(high)-rank(low)+1;

        else return rank(high)-rank(low);

    }
```