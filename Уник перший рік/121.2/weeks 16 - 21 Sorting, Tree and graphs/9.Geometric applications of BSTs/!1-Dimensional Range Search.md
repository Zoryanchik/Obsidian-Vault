![[Pasted image 20250419194044.png]]
```
public List<Key> rangeSearch(Key low, Key high){

    LinkedList<Key> foundList = new LinkedList<Key>();

    if (low.compareTo(high) > 0) throw new IllegalArgumentException(“Incorrect range");

    return rangeSearch(root, low, high, foundList);

}

  
private List<Key> rangeSearch(Node x, Key low, Key high, List<Key> foundList){

    if (x.leftChild != null) foundList = rangeSearch(x.leftChild, low, high, foundList);

    if (x.key.compareTo(low) >= 0 & x.key.compareTo(high) <= 0) foundList.add(x.key);

    if (x.rightChild != null) foundList = rangeSearch(x.rightChild, low, high, foundList);

    return foundList;

}
```
![[Pasted image 20250419194237.png]]
```
private List<Key> rangeSearch(Node x, Key low, Key high, List<Key> foundList){

        if (x.leftChild != null & x.key.compareTo(low) > 0) //low < x.key

  foundList = rangeSearch(x.leftChild, low, high, foundList);

        if (x.key.compareTo(low) >= 0 & x.key.compareTo(high) <= 0) //low = x.key = high      foundList.add(x.key);

        if (x.rightChild != null & x.key.compareTo(high) < 0) //x.key < high

  foundList = rangeSearch(x.rightChild, low, high, foundList);

        return foundList;

    }
```
![[Pasted image 20250419194351.png]]

