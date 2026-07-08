![[Pasted image 20260118195328.png]]![[Pasted image 20260118195451.png]]![[Pasted image 20260118195523.png]]![[Pasted image 20260118195542.png]]![[Pasted image 20260118195740.png]]
Почти всегда с угла, or no correlation
![[Pasted image 20260118195909.png]]![[Pasted image 20260118195930.png]]A **Rainbow Table Attack** is a password cracking method that uses a massive, pre-computed database (the "Rainbow Table") to crack password hashes in seconds or minutes, rather than the years it might take with a standard brute-force attack.

**Answer for your Lab:** "The balance is found by adjusting the **Chain Length** and **Number of Tables**. Longer chains reduce the storage size but increase the CPU time needed to crack the hash. Using more tables increases the success rate (probability of finding the password) but linearly increases the required storage space."
![[Pasted image 20260118200255.png]]![[Pasted image 20260118200601.png]]Here is the easy summary for Question C.2:

**1. The Problem (Too Big)** With your settings (letters `a-Z`, numbers `0-9`, length `1-7`), there are **3.5 trillion** possible passwords. If you wrote them all down in a list, it would take up **80,000 GB** of space. That is too big for most computers.

**2. The Solution (Rainbow Tables)** Rainbow Tables use a math trick (called "chains") to compress that huge list down to about **100 GB**. It trades a little bit of computing power to save a massive amount of disk space.

**3. The Balance (The Answer)** The question asks how to balance storage vs. cracking possibility. Here is the simple rule:

- **Don't aim for perfection:** Trying to crack **100%** of passwords requires a massive file size.
    
- **The Sweet Spot:** If you settle for cracking **99%** of passwords, you can cut the file size in half.
    
- **The Trade-off:**
    
    - **Smaller File:** Takes less space, but takes longer to crack the password.
        
    - **Larger File:** Takes more space, but cracks the password very quickly.
        

**In short:** You balance it by accepting a 99% success rate to save huge amounts of hard drive space.

![[Pasted image 20260118201339.png]]## 1. Bcrypt hash of a sample text

If we input the text **“Hello”** (or **“hello”**) into a Bcrypt Hash Generator (e.g. bcrypt.online) with **cost factor = 10**, the output will look like this:

`$2b$10$eImiTXuWVxfM37uY4JANjQ==Xr8aC0O1E5xE6ZrK8t6Jz8k1fO9e`

⚠️ **Important note:**  
Your hash **will not be identical** to someone else’s hash even if:

- the plaintext is the same (`"Hello"`)
    
- the cost factor is the same (`10`)
    

This is **normal and expected**.

### Why?

Bcrypt automatically generates a **random salt** every time it hashes a password.  
So:

`bcrypt("Hello") ≠ bcrypt("Hello")`

each time you run it.

---

## 2. Input the hash into “Hash Crack”

When you paste a Bcrypt hash (e.g. starting with `$2a$`, `$2b$`, or `$2y$`) into a typical **hash cracking website**, you will find that:

- ❌ The plaintext **cannot be recovered**
    
- ❌ The cracker does **not** output `"Hello"`
    

---

## 3. Why Bcrypt cannot be cracked (in practice)

### Reason 1: Bcrypt is a **one-way function**

Hashing is not encryption.

- Encryption → reversible (with a key)
    
- Hashing → **irreversible**
    

There is **no mathematical way** to “decode” a bcrypt hash.

---

### Reason 2: Built-in **salt**

Each bcrypt hash contains:

- the algorithm version (`$2b$`)
    
- the cost factor (`10`)
    
- a **random salt**
    
- the hash result
    

Because of the salt:

- Precomputed tables (rainbow tables) are useless
    
- The same password produces different hashes
    

---

### Reason 3: **Cost factor (work factor)**

The cost factor controls how slow hashing is.

For cost = 10:

- One hash computation takes noticeable time
    
- Brute-force attacks become extremely slow
    

Higher cost = exponentially more expensive attacks.

Big companies **do not store your real password**. They store a **hash of it** to keep you safe.

Here’s how it works in simple terms 👇
![[Pasted image 20260118201555.png]]## What is actually stored in the database

When you create your password, bcrypt generates **one hash** like this:

`$2b$10$X7s9AqZpR8NQWkM2L9E7uO$h4y8CzY3P1kL9sR2QeXwT`

This single string contains:

- `$2b$` → bcrypt version
    
- `10` → cost factor
    
- `X7s9AqZpR8NQWkM2L9E7uO` → **salt**
    
- `h4y8CzY3P1kL9sR2QeXwT` → hash result
    

👉 **The salt is saved inside the hash itself**

A salt is ==a unique, random string of data added to a password before it is hashed==, ensuring that identical passwords produce different hash results