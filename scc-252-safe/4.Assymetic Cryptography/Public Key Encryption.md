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

![[Pasted image 20260202194727.png]]