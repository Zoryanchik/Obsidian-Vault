![[Pasted image 20250309202736.png]]
![[Pasted image 20250309203253.png]]
![[Pasted image 20250309203514.png]]
Слева наш флоат иза того что мы переводим в инт становиться интом и не материться
Справа чесписс с,  declaring a reference
p = newPrawn is assigning actually this p
c = p all good, p hasnt changed because  p is superclass
![[Pasted image 20250309204546.png]]
![[Pasted image 20250309204636.png]]
-   ![[Pasted image 20250309210242.png]]
- 
    We're calling the  
    parents constructor
- for passing name and  
    age to initialise that.
    We inherate the display from person![[Pasted image 20250309204847.png]]
    But if we have a l1 display in lecturer we gonna use it over from person
    ![[Pasted image 20250309210007.png]]![[Pasted image 20250309205116.png]]- `ChessPiece` is likely a **parent class** (or interface) for different chess pieces (e.g., `Pawn`, `Bishop`, `Knight`).
- The method `canMoveTo(b)` is called on `pieceMoving`, which is of type `ChessPiece`, but the actual method that runs depends on whether `pieceMoving` is a `Pawn`, `Bishop`, etc.
- Each subclass (`Pawn`, `Bishop`, etc.) **overrides** `canMoveTo(b)`, implementing its own movement rules.
![[Pasted image 20250309205400.png]]
![[Pasted image 20250309205426.png]]
![[Pasted image 20250309205554.png]]
![[Pasted image 20250309205609.png]]
it would be 3 