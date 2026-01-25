![[Pasted image 20260123184047.png]]### The Scenario

Imagine we are trying to predict **Test Scores ($y$)** based on **Hours Studied ($x$)**. We have data for 3 students:

- **Student A:** 1 hour, Score 2
    
- **Student B:** 2 hours, Score 4
    
- **Student C:** 3 hours, Score 5
    

So our dataset is:

- $x = [1, 2, 3]$
    
- $y = [2, 4, 5]$
    

---

### Step 1: Calculate the Mean of $x$ and $y$

First, we find the average ($\bar{x}$ and $\bar{y}$) as shown in point 1 of the slide.

$$\bar{x} = \frac{1+2+3}{3} = 2$$

$$\bar{y} = \frac{2+4+5}{3} = \frac{11}{3} \approx 3.67$$

### Step 2: Calculate the Slope ($w$)

We use the formula from point 2: $w = \frac{\sum (x_i - \bar{x})(y_i - \bar{y})}{\sum (x_i - \bar{x})^2}$.

**The Numerator (Top part):** Sum of differences multiplied

- Student A: $(1 - 2)(2 - 3.67) = (-1)(-1.67) = 1.67$
    
- Student B: $(2 - 2)(4 - 3.67) = (0)(0.33) = 0$
    
- Student C: $(3 - 2)(5 - 3.67) = (1)(1.33) = 1.33$
    
- **Sum** $= 1.67 + 0 + 1.33 = 3.0$
    

**The Denominator (Bottom part):** Sum of $x$ differences squared

- Student A: $(1 - 2)^2 = (-1)^2 = 1$
    
- Student B: $(2 - 2)^2 = (0)^2 = 0$
    
- Student C: $(3 - 2)^2 = (1)^2 = 1$
    
- **Sum** $= 1 + 0 + 1 = 2.0$
    

**Calculate $w$:**

$$w = \frac{3.0}{2.0} = 1.5$$

### Step 3: Calculate the Intercept ($b$)

Now we solve for $b$ using the formula from point 3: $b = \bar{y} - w\bar{x}$.

$$b = 3.67 - (1.5 \times 2)$$

$$b = 3.67 - 3 = 0.67$$

### Step 4: Construct the Regression Line

We plug our $w$ and $b$ into the final equation $\hat{y} = wx + b$.

$$\hat{y} = 1.5x + 0.67$$

---

### What does this mean?

The machine has now "learned" the relationship. You can use this model to make a prediction for a new student who studies for **4 hours**:

$$\hat{y} = 1.5(4) + 0.67 = 6.67$$

The model predicts they would get a score of roughly **6.67**.

**Would you like me to explain what happens if the data points are very scattered and don't form a clear line?**

![[Pasted image 20260123185137.png]]![[Pasted image 20260123185238.png]]![[Pasted image 20260123185245.png]]