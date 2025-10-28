Unified Modelling Language (UML)
![[Pasted image 20251028022150.png]]![[Pasted image 20251028022429.png]]![[Pasted image 20251028023106.png]]#### Multiplicity

Multiplicity defines how many instances of one class can be linked to an instance of another class.

- **`1`**: Exactly one.
    
- **`0..1`**: Zero or one.
    
- **`*`** or **`0..*`**: Zero or many.
    
- **`1..*`**: One or many (at least one).
- ![[Pasted image 20251028023153.png]]
- ![[Pasted image 20251028023211.png]]
- #### 1. Association, Aggregation, and Composition

These relationships all show how classes communicate or are linked .

- **Association:** A simple link showing that two classes interact or "talk to" each other .
    
    - _Example:_ A `Student` "learns from" a `Module` .
        
- **Aggregation (Hollow Diamond ♢):** A "has-a" relationship. The part can exist independently of the whole.
    
    - _Example:_ A `Person` works for a `Company`. If the `Company` closes, the `Person` still exists.
        
- **Composition (Solid Diamond ♦):** A strong "part-of" relationship. The part _cannot_ exist without the whole.
    
    - _Example:_ A `Room` is part of a `House`. If the `House` is destroyed, the `Room` is too .

![[Pasted image 20251028023641.png]]This represents an "is-a" relationship. It is shown with a **hollow triangle arrow (△)** pointing from the child class (derived class) to the parent class (abstract class).

- **Abstract Classes:** These classes define methods without implementing all of them. Child classes are then forced to provide the implementations.
    
- Abstract classes and methods are written in _italics_.
    
- An abstract class _can_ provide a default implementation for some methods.
    
- _Example:_ `Cat` and `Dog` are child classes that _extend_ the parent `Animal` class. They inherit the `sleep()` method but must each provide their own implementation of the `sound()` method .

![[Pasted image 20251028023813.png]]#### 3. Realisation (Implements)

This is how a class uses an **Interface**. It is shown with a **dashed line and a hollow triangle arrow (△)** pointing to the interface .

- **Interface:** An interface is a "contract" that _only_ contains method signatures. It specifies _what_ a class must do, but provides no implementation (no code).
    
- A class _must_ implement all methods from the interfaces it "realises".
    
- A single class can implement _multiple_ interfaces, giving it multiple behaviors.
    
- _Example:_ `BubbleSort` and `QuickSort` are different classes that both _realise_ the `Sortable` interface, meaning they both must provide `ascending()` and `descending()` methods .
    

**Interfaces and abstract classes** are a cornerstone of OOP, enabling polymorphism and helping to separate important operations from their specific implementations.![[Pasted image 20251028024529.png]]### How to Draw Class Diagrams

A "Grammatical Approach" can be used to identify parts of a class diagram from a problem description:

- **Nouns (things, roles, locations):** These become **Classes** (e.g., `Customer`, `Account`) or **Attributes** (e.g., `name`, `balance`) .
    
- **Verbs (actions):** These become **Operations** or **Methods** (e.g., `transferFunds()`, `checkBalance()`).
    

When identifying relationships, ask:

- "Is it a subclass of...?" → **Generalisation**
    
- "Is it part of...?" → **Aggregation** or **Composition**
    
- "Does it interact with...?" → **Association**
    

**Important:** The lecture slides note that you will be expected to use **PlantUML** for your diagrams.