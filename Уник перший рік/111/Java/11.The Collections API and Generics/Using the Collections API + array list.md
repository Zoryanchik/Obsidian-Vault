![[Pasted image 20250414154104.png]]🔍 What’s happening here?

- `ArrayList<Person> staff`  
    ➤ Declares a list to store `Person` objects.  
    ➤ The red arrow and text explain that `Person` is the **type of things you want to store**.
    
- `new ArrayList<>()`  
    ➤ Instantiates the list. Since the type is already specified on the left, it can be omitted on the right (Java 7+ feature called **type inference**).
    
- `staff.add(...)`  
    ➤ Adds `Person` objects to the list using the `.add()` method.

![[Pasted image 20250414154805.png]]
You can loop through collections using:

`for (Person p : staff)`
![[Pasted image 20250414155440.png]]
