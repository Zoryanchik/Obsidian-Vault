![[Pasted image 20260112020355.png]]![[Pasted image 20260112020419.png]]![[Pasted image 20260112020453.png]]![[Pasted image 20260112020527.png]]![[Pasted image 20260112020541.png]]![[Pasted image 20260112020611.png]]![[Pasted image 20260112020624.png]]![[Pasted image 20260112020655.png]]![[Pasted image 20260112020803.png]]![[Pasted image 20260112020840.png]]![[Pasted image 20260112021651.png]]![[Pasted image 20260112021711.png]]In the context of the UML class diagram you've provided, **aggregation** is represented by the **hollow diamond shape** (⋄) at the end of the association lines.

Aggregation is a "part-of" relationship where the "part" can exist independently of the "whole." In this specific ATM system, here is how it is being used:

## Where Aggregation Appears

The diagram shows that the **ATM** class is the "whole," and it aggregates several hardware components. Specifically:

- **ATM ⋄— Display_Keypad:** The ATM "has a" display and keypad.
    
- **ATM ⋄— Cash_Dispenser:** The ATM "has a" cash dispenser.
    
- **ATM ⋄— Card_Reader:** The ATM "has a" card reader.
    
- **ATM ⋄— Printer:** The ATM "has a" printer.
    

Additionally, there is an aggregation between **CustomerDB** and **CustomerAccount**:

- **CustomerDB ⋄— CustomerAccount:** The database "has" accounts, but logically, an account's data exists as a separate entity within that database.