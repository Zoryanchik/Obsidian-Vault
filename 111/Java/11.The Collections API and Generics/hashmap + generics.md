![[Pasted image 20250414155751.png]]![[Pasted image 20250414160116.png]]> _“Classes can be parameterised, just like functions and methods!”_

That means instead of writing a class for every data type (like `Integer`, `String`, `Person`, etc.), you write it **once** using a placeholder type — for example, `E` — and later replace `E` with the actual type when you use it.

LinkedList<String> stringList = new LinkedList<>();
LinkedList<Integer> intList = new LinkedList<>();
