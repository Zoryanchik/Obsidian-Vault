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
![[Pasted image 20260125231110.png]]
### 1. The Core Mechanism

In CFB, we don't actually encrypt the message directly with the block cipher algorithm. Instead, we encrypt the **previous ciphertext** and then mix it with our message.

- **Step 1:** The algorithm encrypts the **Initialization Vector (IV)** (for the first block) or the **previous ciphertext block** ($c_{n-1}$) using the key ($k$).
    
- **Step 2:** The result of that encryption is then **XORed** ($\oplus$) with the current plaintext block ($m_n$).
    
- **Step 3:** This creates the ciphertext block ($c_n$), which is then "fed back" into the next stage to be encrypted.
 
![[Pasted image 20260125231350.png]]
You've hit the "speed demon" of the group. **Counter (CTR) Mode** is currently one of the most popular modes because it is incredibly fast and efficient.

While CBC and CFB were "chains" (where you had to wait for one block to finish before starting the next), CTR mode is all about **parallelism**.

### 1. How it Works

Instead of using the previous ciphertext to mix with the next block, it uses a simple **Counter** ($ctr$).

- **The Keystream:** For every block, a unique counter value ($ctr_1, ctr_2, \dots$) is encrypted with the key ($k$).
    
- **The XOR:** The output of that encryption is then XORed ($\oplus$) with your message block ($m_n$) to produce the ciphertext ($c_n$).
    
- **Math:** $c_i = m_i \oplus E_k(ctr_i)$.
    

---

### 2. Why is this better?

Imagine you have a 4-core processor. In CBC mode, three cores sit idle while the first core finishes block 1. In **CTR mode**, you can give block 1 to Core A, block 2 to Core B, and so on, because the counter values are known in advance.

- **Speed:** It is massively parallelizable.
    
- **Random Access:** If you only need to decrypt the 50th block of a file, you can jump straight there without decrypting the first 49 blocks.
In the context of **Counter (CTR) Mode**, the "counter value" ($ctr$) is a unique, non-repeating number that acts as the input for the encryption algorithm.

![[Pasted image 20260125232055.png]]
**![[Pasted image 20260125231826.png]]
b**

![[Pasted image 20260125232249.png]]![[Pasted image 20260125232340.png]]

HMAC = hash(message + secret key), done twice, to guarantee integrity and authenticity

![[Pasted image 20260125232504.png]]CBC-MAC = run CBC encryption (with IV=0) and take the last block as the authentication tag

![[Pasted image 20260125232531.png]]
