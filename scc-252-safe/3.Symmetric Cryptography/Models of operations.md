![[Pasted image 20260125230817.png]]
![[Pasted image 20260125230747.png]]
This slide covers **Electronic Code Book (ECB)**, which is the most basic way to use a block cipher (like AES) to encrypt a long message.

This slide covers **Electronic Code Book (ECB)**, which is the most basic way to use a block cipher (like AES) to encrypt a long message.

Think of it like a **literal translation**: if you always translate the word "Apple" into "123," every time "Apple" appears in your book, the reader sees "123."

Here is the breakdown of what you actually need to know for your studies:

### 1. The Core Concept

A message is usually too long to encrypt all at once, so we chop it into fixed-size pieces called **blocks** (m1​,m2​,…). In ECB mode:

- Each block is encrypted **independently**.
    
- The **same key (k)** is used for every single block.
    
- The math is simply: ci​=Ek​(mi​).
    

 Because each block is handled in isolation, if $m_1$ and $m_2$ are exactly the same, $c_1$ and $c_2$ will be exactly the same.
![[Pasted image 20260125230755.png]]
In CBC mode, each block of text is "mixed" with the block that came before it before it gets encrypted.

- **The Chain:** Before a plaintext block ($m_n$) is encrypted, it is combined with the previous ciphertext block ($c_{n-1}$) using an **XOR** operation (the $\oplus$ symbol in the diagram).
    
- **The Result:** Because every block depends on the one before it, even if you have two identical plaintext blocks (like two "Apples"), their ciphertexts will look completely different. This successfully **breaks up patterns** that were visible in ECB.
### 2. The Role of the Initialization Vector (IV)

You might notice a problem: the very first block ($m_1$) doesn't have a "previous ciphertext" to mix with.

- **The Solution:** We use an **Initialization Vector (IV)**.
    
- **Purpose:** The IV is a random block of data used to start the process for the first block. This **ensures uniqueness**—even if you encrypt the exact same message twice with the same key, using a different IV will result in completely different ciphertext. 
![[Pasted image 20260125231110.png]]![[Pasted image 20260125231350.png]]
## 1️⃣ ECB — Electronic Codebook (❌ insecure)

**How it works**

- Each block is encrypted **independently**
    
- Same plaintext block → same ciphertext block
    

**Properties**

- ❌ No IV
    
- ❌ Leaks patterns
    
- ❌ Not semantically secure
    

**Visual intuition**

`P1 → E → C1 P2 → E → C2 P1 → E → C1   (same input → same output)`

**When to use**

- ❌ Never for real data
    
- ✔️ Only for learning
    

---

## 2️⃣ CBC — Cipher Block Chaining (⚠️ legacy but better)

**How it works**

- Each plaintext block is XORed with the **previous ciphertext block**
    
- Uses an **IV** for the first block
    

`C1 = E(P1 ⊕ IV) C2 = E(P2 ⊕ C1) C3 = E(P3 ⊕ C2)`

**Properties**

- ✔️ Hides patterns
    
- ✔️ Widely used historically
    
- ❌ Not parallelizable (encryption)
    
- ❌ Vulnerable to padding oracle attacks if used wrong
    

**When to use**

- ⚠️ Legacy systems only
    
- ❌ Avoid in new designs
    

---

## 3️⃣ CFB — Cipher Feedback (stream-like)

**How it works**

- Turns a block cipher into a **stream cipher**
    
- Encrypts previous ciphertext and XORs with plaintext
    

`E(IV) ⊕ P1 → C1 E(C1) ⊕ P2 → C2`

**Properties**

- ✔️ No padding needed
    
- ✔️ Works on small chunks
    
- ❌ Error propagation
    
- ❌ Slower than CTR
    

**When to use**

- Streaming data (older protocols)
    

---

## 4️⃣ CTR — Counter Mode (✅ modern & fast)

**How it works**

- Encrypts a **counter + nonce**
    
- XORs result with plaintext
    

`E(nonce || counter) ⊕ plaintext`

**Properties**

- ✔️ Very fast
    
- ✔️ Fully parallelizable
    
- ✔️ No padding
    
- ❌ **Nonce reuse = catastrophic**
    

**When to use**

- Modern systems (if nonce is guaranteed unique)
![[Pasted image 20260125232055.png]]
**![[Pasted image 20260125231826.png]]
b**

![[Pasted image 20260125232249.png]]![[Pasted image 20260125232340.png]]

HMAC = hash(message + secret key), done twice, to guarantee integrity and authenticity

![[Pasted image 20260125232504.png]]CBC-MAC = run CBC encryption (with IV=0) and take the last block as the authentication tag

![[Pasted image 20260125232531.png]]
