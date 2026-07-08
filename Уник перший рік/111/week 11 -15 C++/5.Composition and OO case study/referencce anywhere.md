![[Pasted image 20250208213453.png]]
#### **Explanation**:

1. **Valid Use of References**:
    - The parameter `Car &c` passes a reference to the original object (no copy is made).
    - `Car &sameCar = c;` creates a new reference `sameCar` that refers to the same object as `c`.
2. **Behavior**:
    - Changes made via `c` or `sameCar` will directly affect the original object passed to the function.
3. **Result**:
    - This code is valid and works as intended.
![[Pasted image 20250208213725.png]]
#### **Explanation**:

1. **References Require Initialization**:
    - A reference in C++ must be initialized at the time of declaration (e.g., `Car &sameCar = c;`).
    - The line `Car &sameCar;` attempts to declare a reference without initialization, which is **illegal** in C++.
2. **Assignment Does Not Work**:
    - The statement `sameCar = c;` does not initialize `sameCar` as a reference. Instead, it tries to assign the value of `c` to whatever `sameCar` is referencing, which is undefined behavior since `sameCar` is not initialized.

#### **Result**:

- This code is **invalid** and will not compile.
![[Pasted image 20250208213544.png]]
#### **Explanation**:

1. **Global References Require Initialization**:
    - Like local references, global references must also be initialized when declared.
    - `Car &sameCar;` is illegal because it lacks initialization.
2. **Assignment Does Not Initialize**:
    - The line `sameCar = c;` does not initialize `sameCar` as a reference. Instead, it assigns the value of `c` to whatever `sameCar` refers to. Since `sameCar` is uninitialized, this leads to undefined behavior.
![[Pasted image 20250208214324.png]]
This is legal