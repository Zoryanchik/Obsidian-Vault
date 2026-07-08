![[Pasted image 20260111191314.png]]# SCC211 – Software Design

## Design Patterns 2: Builder, Template Method, Façade

---

## 1. Builder Pattern (Creational)

### Intent

The **Builder pattern** separates the **construction** of a complex object from its **representation**, allowing the same construction process to create different representations.

### Motivation

- Complex objects often require multiple construction steps
    
- Different versions share the same construction logic
    
- Avoids large constructors and complex conditionals
    

### Key Idea

- Construction is split into **steps**
    
- Steps are implemented by **Builder classes**
    
- A **Director** controls the order of construction
    
- The finished **Product** is retrieved from the Builder
    

### Participants

- **Product** – the complex object being built
    
- **Builder (abstract / interface)** – defines construction steps
    
- **ConcreteBuilder** – implements steps for a specific representation
    
- **Director** – controls the building process
    

### Structure

1. Client selects a ConcreteBuilder
    
2. Director invokes construction steps in order
    
3. Builder constructs and returns the Product

![[Pasted image 20260111191749.png]]![[Pasted image 20260111191901.png]]![[Pasted image 20260111192000.png]]![[Pasted image 20260111192126.png]]![[Pasted image 20260111193021.png]]![[Pasted image 20260111193156.png]]![[Pasted image 20260111193208.png]]![[Pasted image 20260111193403.png]]![[Pasted image 20260111195150.png]]![[Pasted image 20260111195214.png]]