![[Pasted image 20251222144123.png]]### 1. Functional vs. Structural Mental Models

- **Structural Mental Model:** This is an internal understanding of **how a system works** internally. It includes knowledge of the components, their relationships, and the underlying mechanics (e.g., knowing how an internal combustion engine works).
    
- **Functional Mental Model:** This is an understanding of **how to use a system** to achieve a goal. It is task-oriented and based on "if-then" procedures rather than internal mechanics (e.g., knowing that turning the key starts the car).
    

**Example:** A **Microwave Oven**. Most people have a _functional_ model: they know that pressing "Start" and "30s" makes food hot. However, very few have a _structural_ model: most don't know how the magnetron generates microwaves or how the waveguide directs them.

---

### 2. Mental Model vs. Conceptual Model

- **Mental Model:** The internal, subjective representation that a **user** forms in their mind about how a system works. It is often incomplete or even technically "wrong," but it guides their behavior.
    
- **Conceptual Model:** The high-level description of how a system is organized and operates, created by the **designer**. It is the "correct" way the designer intends for the user to perceive the system (e.g., the "Desktop" metaphor in Windows/macOS).
    

> **Crucial Difference:** A designer uses a conceptual model to build the interface, hoping the user will develop a mental model that matches it.

---

### 3. Three Types of Interaction Errors

Don Norman’s framework is often used here:

1. **Slips:** These occur when a user has the right intention but performs the wrong action due to a lapse in attention (e.g., intending to click "Save" but clicking "Cancel" because they are in a hurry).
    
2. **Lapses:** These are memory-based failures where a user forgets to perform a step in a process (e.g., forgetting to take the original document out of the scanner after making a copy).
    
3. **Mistakes:** These occur when a user has the wrong goal or plan because their mental model of the system is incorrect (e.g., trying to "save" a document by closing the window, believing it autosaves when it actually doesn't).
    

---

### 4. Errors due to UI Inconsistency

When a UI is inconsistent with other apps, **Slips** (specifically **Capture Errors**) become much more likely.

**Explanation:** This is due to **Negative Transfer**. Users develop "muscle memory" or habits from other applications. If most apps place the "Delete" button in the bottom right, but your app places "Submit" there, a user may reflexively click "Submit" when they intended to delete something. Their habit "captures" their behavior, leading to a slip because the interface did not meet their established expectations.

---

Would you like me to create a practice scenario to help you test your ability to distinguish between slips and mistakes?