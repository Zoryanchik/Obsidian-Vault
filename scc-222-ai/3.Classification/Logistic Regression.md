![[Pasted image 20260130194929.png]]![[Pasted image 20260130195030.png]]![[Pasted image 20260130195040.png]]![[Pasted image 20260130195059.png]]![[Pasted image 20260130195107.png]]![[Pasted image 20260130195208.png]]![[Pasted image 20260130195223.png]]![[Pasted image 20260130195252.png]]![[Pasted image 20260130195342.png]]### 1. The Left Graph: Predicting Log-Odds (The Linear Part)

The graph on the left visualizes the "internal" math of the model before it outputs a probability.

- **X-Axis:** Hours of revision (0 to 10).
    
- **Y-Axis:** Log-odds (also called the "logit"). Unlike probability, which is stuck between 0 and 1, log-odds can range from $-\infty$ to $+\infty$.
    
- **The Line:** The dashed grey line represents a linear equation ($z = mx + c$). In this specific example, the equation is $z = 1.108x - 5.129$.
    
    - This line predicts the **log-odds** of passing.
        
    - **Key Insight:** Notice the pink dotted line at $y=0$. This is the decision boundary. When the log-odds are 0, the probability is exactly 0.5 (50%).
        
    - **The Math:** The text explicitly calculates specific points. For example, a probability ($p$) of 0.8 corresponds to a log-odds of 1.386.
        

### 2. The Center Box: The Sigmoid Transformation

The orange box in the middle is the bridge between the two graphs. It contains the **Sigmoid Function** formula:

$$p(y=1) = \sigma(z) = \frac{1}{1 + e^{-z}}$$

This function takes the unbounded value $z$ (the result of the linear equation on the left) and "squashes" it to ensure the result is always between 0 and 1.

### 3. The Right Graph: Probability (The S-Curve)

The graph on the right shows the final output that humans usually interpret.

- **Y-Axis:** Probability of Pass (0.0 to 1.0).
    
- **The Curve:** The linear line from the left graph has been bent into an "S" shape (the sigmoid curve).
    
    - **Low Revision (0-2 hours):** The curve is near 0. The model is confident you will fail.
        
    - **High Revision (7+ hours):** The curve is near 1. The model is confident you will pass.
        
    - **The Transition:** Between 4 and 5 hours, the curve rises steeply. This is the area of uncertainty where a small increase in revision hours drastically increases the probability of passing.

![[Pasted image 20260130195535.png]]![[Pasted image 20260130195602.png]]![[Pasted image 20260130195628.png]]Based on the second slide provided, here is an explanation of the **Log-Loss function** (also known as Cross Entropy Loss), which is the standard way to measure error in logistic regression.

This slide answers the question: _"How do we mathematically calculate how 'wrong' our model is?"_

### 1. The Purpose of Log-Loss

The main goal of this function is to **penalize confidence in wrong predictions**.

- If the model predicts a probability close to the true value (e.g., predicting 0.9 when the answer is 1), the loss (error) is **small**.
    
- If the model predicts a probability far from the true value (e.g., predicting 0.1 when the answer is 1), the loss is **very large**.
    

### 2. The Conditional Logic (Top Half)

The slide breaks the loss down into two specific scenarios based on the true label ($y_i$):

#### **Case A: The True Answer is 1 ($y_i = 1$)**

- **Formula:** $\text{Loss} = -\log(\hat{y}_i)$
    
- **Visual (Blue Curve):** Look at the graph on the right. If the true value is 1 (Blue line), you want your prediction ($\hat{y}_i$) to be near 1.
    
    - As $\hat{y}_i \to 1$, the loss drops to 0.
        
    - As $\hat{y}_i \to 0$, the loss shoots up to infinity (massive penalty for being dead wrong).
        

#### **Case B: The True Answer is 0 ($y_i = 0$)**

- **Formula:** $\text{Loss} = -\log(1 - \hat{y}_i)$
    
- **Visual (Red Curve):** If the true value is 0 (Red line), you want your prediction to be near 0.
    
    - As $\hat{y}_i \to 0$, the loss drops to 0.
        
    - As $\hat{y}_i \to 1$, the loss shoots up to infinity.
        

### 3. The Combined Formula (Bottom Red Box)

Instead of writing "If/Else" statements in our code or math, we combine both cases into a single, elegant equation:

$$\text{Log-loss} = -\frac{1}{m} \sum_{i=1}^{m} [y_i \log(\hat{y}_i) + (1 - y_i) \log(1 - \hat{y}_i)]$$

**Why this works (The "Switch" Trick):**

- **When $y_i = 1$:** The second part of the equation $(1 - y_i)$ becomes 0, cancelling it out. We are left with just the first part: $\log(\hat{y}_i)$.
    
- **When $y_i = 0$:** The first part $y_i \log(\hat{y}_i)$ becomes 0. We are left with just the second part: $\log(1 - \hat{y}_i)$.

- **$m$**: Total number of training examples (how much data you have).
    
- **$y_i$**: The **actual** truth (0 or 1).
    
- **$\hat{y}_i$**: The **predicted** probability output by your sigmoid function (between 0 and 1).
    
- **$\log$**: The natural logarithm (base $e$).

![[Pasted image 20260130195929.png]]
