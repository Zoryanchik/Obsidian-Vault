![[Pasted image 20250208211831.png]]
![[Pasted image 20250208212527.png]]![[Pasted image 20250208212008.png]]![[Pasted image 20250208212105.png]]![[Pasted image 20250208212637.png]]![[Pasted image 20250208212713.png]]### **Key Differences**:

1. **Pass-by-Pointer**:
    
    - In this example, the object is passed to the function as a **pointer** (`Car *c`), not as a copy.
    - The pointer `c` points to the memory address of the original object (`joesPassat`).
2. **Direct Modification**:
    
    - Since `c` points to the same memory address as `joesPassat` (`0x7ffeefbff590`), any modifications made to `c` inside the `goOnHoliday` function will affect the original object (`joesPassat`).
3. **Function Call**:
    
    - Instead of passing the object directly, a pointer to the object is passed using the `&` operator in `goOnHoliday(&joesPassat);`.
4. **Arrow Operator (`->`)**:
    
    - Inside the `goOnHoliday` function, the arrow operator (`->`) is used to access methods or properties of the object through the pointer `c`.

![[Pasted image 20250208213213.png]]
![[Pasted image 20250208213249.png]]
1000 same as pointer kind of но это именно референс

