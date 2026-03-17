![[Pasted image 20260317083408.png]]![[Pasted image 20260317083751.png]]![[Pasted image 20260317083815.png]]![[Pasted image 20260317084005.png]]![[Pasted image 20260317084051.png]]the smaller the better
![[Pasted image 20260317084307.png]]![[Pasted image 20260317084442.png]]![[Pasted image 20260317084521.png]]![[Pasted image 20260317084532.png]]_"If a new data point falls on the right side of this line, you can confidently predict that it is a Class 2 green dot."_ W
![[Pasted image 20260317084723.png]]Let’s build a brand new, simplified example from scratch to make sure you have the mechanics locked down.

Imagine we are building a decision tree to classify **Power Tools**. We want the algorithm to look at some data and predict whether a tool is a **Drill (Class 1)** or a **Circular Saw (Class 2)**.

### 1. The Starting Dataset

We have a small dataset of 4 tools sitting on the workbench:

- **Total ($S$):** 4 tools
    
- **Class 1 (Drills):** 2 tools
    
- **Class 2 (Saws):** 2 tools
    

**Baseline Entropy:**

Since the group is exactly a 50/50 split, our uncertainty is at its absolute maximum.

$$E(S) = 1.0$$

---

### 2. Testing Split Option A: Weight $\le 3$ kg

The algorithm needs to find the best question to separate the drills from the saws. First, it tries splitting them by weight.

Let's say all 2 drills weigh less than 3 kg, and all 2 saws weigh more than 3 kg.

- **Left Branch ($C_1$, Weight $\le 3$ kg):** Gets 2 tools (both Drills). Because it is purely drills, the entropy is **$0$**.
    
- **Right Branch ($C_2$, Weight $> 3$ kg):** Gets 2 tools (both Saws). Because it is purely saws, the entropy is **$0$**.
    

**Weighted Average Entropy:**

$$E(Option A) = \frac{(2 \times 0) + (2 \times 0)}{4} = 0$$

**Information Gain:**

$1.0$ (Starting Entropy) $- 0$ (New Entropy) = **$1.0$**

---

### 3. Testing Split Option B: Cordless? (Yes/No)

Now, the algorithm tests a different feature to see if it's better. It splits them based on whether they are battery-powered (Cordless) or plug-in.

Let's say 1 Drill and 1 Saw are Cordless, and the other Drill and Saw are Plug-in.

- **Left Branch ($C_1$, Cordless = Yes):** Gets 2 tools (1 Drill, 1 Saw). This is still a 50/50 split, so the entropy is **$1.0$**.
    
- **Right Branch ($C_2$, Cordless = No):** Gets 2 tools (1 Drill, 1 Saw). Also a 50/50 split, so the entropy is **$1.0$**.
    

**Weighted Average Entropy:**

$$E(Option B) = \frac{(2 \times 1.0) + (2 \times 1.0)}{4} = 1.0$$

**Information Gain:**
1.o that we times is Es 
![[Pasted image 20260317085424.png]]

$1.0$ (Starting Entropy) $- 1.0$ (New Entropy) = **$0$**

---

### 4. The Final Decision

The ID3 algorithm compares the Information Gain of both options:

- **Weight:** Gain of $1.0$
    
- **Cordless:** Gain of $0$
    

The algorithm permanently chooses **Weight** as the Root Node because it provides the biggest reduction in messiness. Furthermore, because both branches resulting from the "Weight" split have an entropy of $0$, the algorithm stops completely. It creates two Leaf Nodes: a "1" on the left (predict Drill) and a "2" on the right (predict Saw).

Does setting it up with this power tool scenario help clarify how the algorithm uses the math to make physical branching decisions?
![[Pasted image 20260317085113.png]]