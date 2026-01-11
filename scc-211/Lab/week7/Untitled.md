![[Pasted image 20260111203647.png]]
![[Pasted image 20260111204255.png]]![[Pasted image 20260111204342.png]]![[Pasted image 20260111203655.png]]
![[Pasted image 20260111204820.png]]
![[Pasted image 20260111205005.png]]
![[Pasted image 20260111205020.png]]
![[Pasted image 20260111205036.png]]
![[Pasted image 20260111205103.png]]
# SCC.204 Software Design Workshop

## Solved Problems: Observer & Adapter Patterns

---

## Problem 1 – Observer Pattern: Traffic Lights 🚦

### Problem Summary

Cars are waiting at traffic lights. When the traffic light changes state (e.g. RED → GREEN), **all cars must be notified automatically**.

This is a classic **Observer pattern** scenario.

---

### Pattern Mapping

|Observer Pattern Role|Traffic Light Example|
|---|---|
|Subject|TrafficLight|
|Observer|Car|
|ConcreteSubject|TrafficLight|
|ConcreteObserver|Car|

---

### Class Responsibilities

#### Subject (TrafficLight)

- Maintains a list of cars (observers)
    
- Notifies cars when state changes
    

Methods:

- addObserver(Car)
    
- removeObserver(Car)
    
- notifyObservers()
    
- changeState()
    

#### Observer (Car)

- Receives updates from TrafficLight
    

Method:

- update(String lightState)
    

---

### UML-style Class Diagram (Textual)

```
<<interface>> Observer
+ update(state)

Car
+ update(state)

<<interface>> Subject
+ addObserver(o)
+ removeObserver(o)
+ notifyObservers()

TrafficLight
- observers : List<Observer>
- state : String
+ addObserver(o)
+ removeObserver(o)
+ notifyObservers()
+ changeState()

TrafficLight 1 ---- * Car
```

---

### How It Works (Exam Explanation)

1. Cars register themselves with the TrafficLight
    
2. TrafficLight changes state (e.g. GREEN)
    
3. TrafficLight calls notifyObservers()
    
4. All cars receive update() and react
    

---

### Why Observer Fits

- Loose coupling between cars and traffic lights
    
- Automatic updates
    
- Easy to add/remove cars
    

---

## Problem 2 – Adapter Pattern: Banner Printing 🖨️

### Problem Summary

Clients want to use a **Banner** class, but their required interface is different.

- Banner provides:
    
    - showWithParenthesis()
        
    - showWithAsterisks()
        
- Clients expect:
    
    - printWeak()
        
    - printStrong()
        

Solution: **Adapter Pattern**

---

## Adapter Solution 1 – Class Adapter (Inheritance)

### Structure

- Adapter inherits from Banner
    
- Adapter implements Print interface
    

### UML-style Diagram

```
Print (interface)
+ printWeak()
+ printStrong()

Banner
+ showWithParenthesis()
+ showWithAsterisks()

PrintBanner
extends Banner
implements Print
+ printWeak()
+ printStrong()

Client ---> Print
```

### How It Works

- printWeak() → showWithParenthesis()
    
- printStrong() → showWithAsterisks()
    

---

## Adapter Solution 2 – Object Adapter (Composition)

### Structure

- Adapter contains a Banner object
    
- Adapter implements Print interface
    

### UML-style Diagram

```
Print (interface)
+ printWeak()
+ printStrong()

Banner
+ showWithParenthesis()
+ showWithAsterisks()

PrintBanner
- banner : Banner
+ printWeak()
+ printStrong()

Client ---> Print
```

---

### How It Works

- Adapter translates client calls into Banner calls
    
- Client remains unaware of Banner implementation
    

---

## Why Adapter Fits

- Allows incompatible interfaces to work together
    
- No need to modify Banner class
    
- Supports reuse of existing code
    

---

## Exam-Ready One-Line Answers

**Observer:**

> The Observer pattern defines a one-to-many dependency where observers are notified automatically when the subject changes state.

**Adapter:**

> The Adapter pattern converts the interface of a class into another interface expected by clients.

---

## Quick Comparison Table

|Pattern|Type|Purpose|
|---|---|---|
|Observer|Behavioral|Notify multiple objects of state change|
|Adapter|Structural|Make incompatible interfaces compatible|

---

✅ End of Solved Workshop Problems