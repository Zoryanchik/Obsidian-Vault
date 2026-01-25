![[Pasted image 20260125230817.png]]
![[Pasted image 20260125230747.png]]
![[Pasted image 20260125230755.png]]![[Pasted image 20260125231110.png]]![[Pasted image 20260125231350.png]]
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
