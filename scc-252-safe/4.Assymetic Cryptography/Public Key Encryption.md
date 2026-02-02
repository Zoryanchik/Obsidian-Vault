![[Pasted image 20260202190837.png]]### 2. Diffie-Hellman Key Exchange

**What is it?**

This protocol solves a major problem: How do two people (Alice and Bob) agree on a secret key over the internet without someone listening in and stealing it? It is used to "securely exchange a key".

**How it works (The Process):**

The slide illustrates a conversation between Alice and Bob:

1. **Public Parameters:** Everyone knows two numbers: a prime number $p$ and a generator $g$.
    
2. **Private Secrets:**
    
    - Alice picks a secret number $a$ (from $1$ to $p-1$).
        
    - Bob picks a secret number $b$ (from $1$ to $p-1$).
        
3. **Public Exchange:**
    
    - Alice calculates $X_a = g^a$ and sends it to Bob.
        
    - Bob calculates $X_b = g^b$ and sends it to Alice.
        
4. **The Magic (Shared Secret):**
    
    - Alice takes Bob's number and uses her secret: $K = (X_b)^a$.
        
    - Bob takes Alice's number and uses his secret: $K = (X_a)^b$.
        
    - Because of the math shown in the slide ($(g^b)^a = (g^a)^b$), they both end up with the **exact same number** $K$, which becomes their shared secret key.
        

**Why is it secure?**

The security relies on the **Discrete Logarithm Problem**. The slide explains that even if a hacker knows the public elements ($a, b, p$), it is mathematically "hard" to figure out the secret exponent ($x$) in the equation $a^x \equiv b \mod p$. Essentially, mixing the numbers is easy, but un-mixing them is nearly impossible without the private key.

![[Pasted image 20260202191308.png]]
![[Pasted image 20260202191754.png]]![[Pasted image 20260202191942.png]]![[Pasted image 20260202192040.png]]![[Pasted image 20260202192431.png]]![[Pasted image 20260202193543.png]]![[Pasted image 20260202194150.png]]

![[Pasted image 20260202194727.png]]![[Pasted image 20260202195608.png]]![[Pasted image 20260202201852.png]]![[Pasted image 20260202203525.png]]### 1. What is "Deterministic"?

In the context of encryption, **deterministic** means that the same input always creates the exact same output.

- **The Scenario:** If you encrypt the word "Hello" today, and then encrypt the word "Hello" again tomorrow using the same key, the resulting ciphertext will look **identical**.
    
- **The Problem:** This is a security weakness. If an attacker sees the same ciphertext twice, they immediately know you sent the same message twice. It reveals patterns in your communication without them even needing to crack the code.
    

### 2. What is "Padding"?

**Padding** is the solution used to fix the "deterministic" problem. It involves adding random data to your message _before_ you encrypt it.

- **The Fix:** instead of just encrypting "Hello", the system automatically adds random numbers to it (e.g., "Hello + _random284_").
    
- **The Result (Probabilistic Encryption):**
    
    - **Attempt 1:** Encrypts "Hello + _random284_" $\rightarrow$ Output is `Xy7z...`
        
    - **Attempt 2:** Encrypts "Hello + _random991_" $\rightarrow$ Output is `Ab3q...`
        
- **Why it matters:** Even though the core message is the same, the encrypted text looks completely different every time. This hides patterns from attackers.
    

**Summary:**

The slide states that because RSA is naturally **deterministic** (predictable), you _must_ use a **padding scheme** to make it **probabilistic** (random/unpredictable) and secure.

**Would you**

![[Pasted image 20260202203738.png]]
idk![[Pasted image 20260202203804.png]]