![[Pasted image 20251113003315.png]]![[Pasted image 20251113003326.png]]![[Pasted image 20251113003408.png]]- **Single Responsibility Principle (SRP)**: Vet class has multiple reasons to change (adding new animal types requires modifying Vet)
- **Open/Closed Principle (OCP)**: Not open for extension - adding new animals requires modifying Vet class
- **Interface Segregation Principle (ISP)**: Potentially forces clients to depend on methods they don't use
- **Dependency Inversion Principle (DIP)**: Vet depends on concrete classes (Cat, Dog) rather than abstractions
![[Pasted image 20251113003512.png]]![[Pasted image 20251113003638.png]]This design violates the **Interface Segregation Principle (ISP)**, which states that "no client should be forced to depend on methods it does not use."

**The Issue**:

- `UserClient` only needs `uploadFile()` and `downloadFile()`
- But it's forced to depend on the entire `FileServer` interface, including `changePermissions()`
- This creates unnecessary coupling and potential for misuse
![[Pasted image 20251113004043.png]]![[Pasted image 20251113004121.png]]![[Pasted image 20251113004321.png]]


