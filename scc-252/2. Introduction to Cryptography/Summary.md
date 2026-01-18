Based on the learning outcomes outlined in the lecture slides1, here is a detailed summary of the key topics covered:

### 1. Security Services and Cryptographic Systems

This section covers the specific goals of security and the systems used to achieve them.

- **Core Security Services:**
    
    - **Confidentiality:** Ensuring data is not viewed by unauthorized entities2.
        
    - **Data Integrity:** Ensuring data is not altered in an unauthorized manner3.
        
    - **Data Origin Authentication:** Verifying the identity of the entity that created the data4.
        
    - **Non-repudiation:** Preventing an entity from denying a previous action5.
        
    - **Other Services:** Accountability, Anonymity, and Verifiability666666666.
        
        +2
        
- **System Capabilities:**
    
    - **Encryption Systems:** primarily provide confidentiality7.
        
    - **Hash Functions:** provide integrity but not confidentiality or non-repudiation8.
        
    - **Digital Signatures:** provide integrity, authentication, and non-repudiation9.
        

### 2. Basic Operations of Cryptographic Schemes

The lecture defines the mathematical structure and flow of encryption and signatures.

- **Encryption Schemes:**
    
    - Defined as a tuple $(P, C, K, Enc, Dec)$ consisting of plaintext space, ciphertext space, key space, and encryption/decryption functions10.
        
    - It requires that for every encryption key, there exists a decryption key such that the original message is recoverable: $Dec_{dk}(Enc_{ek}(m))=m$11.
        
    - Security relies on **Kerckhoff's Principle**: the system must remain secure even if everything (algorithms, etc.) except the key is public knowledge12.
        
- **Signature Schemes:**
    
    - Involve a **signing key** ($sk$) used by the sender to create a signature $\sigma$ using a signing algorithm131313131313131313.
        
        +2
        
    - Involve a **verification key** ($vk$) used by the receiver to validate the message and signature using a verification algorithm14141414.
        
        +1
        
    - These schemes aim to provide data integrity, authentication, and non-repudiation15.
        

### 3. Potential Attacks and Security Levels

Understanding how systems are compromised is essential for designing secure systems.

- **Attack Categories:**
    
    - **Passive Attacks:** The attacker does not alter data. Examples include unauthorized access to data and traffic analysis16.
        
    - **Active Attacks:** The attacker modifies data or processes. Examples include masquerade, replay attacks, and modification of data171717171717171717.
        
        +2
        
- **Specific Encryption Attacks:**
    
    - **Ciphertext-only:** Attacker knows only ciphertexts18.
        
    - **Known-plaintext:** Attacker knows some plaintext/ciphertext pairs19.
        
    - **Chosen-plaintext:** Attacker can choose plaintexts and see the corresponding ciphertexts20. Modern systems must withstand this21.
        
        +1
        
- **Signature Forgery:**
    
    - **Existential Unforgeability:** The goal is to prevent an attacker from generating a valid signature for _any_ message they choose22.
        

### 4. Cryptographic Hash Functions

Hash functions are versatile algorithms used for compressing data into unique fixed-length outputs.

- **Definition:** A function $h:\{0,1\}^{*}\rightarrow\{0,1\}^{n}$ that maps an input of any size to a fixed length output and is easy to compute23232323.
    
    +1
    
- **Required Properties:**
    
    - **Preimage Resistance:** Given hash $y$, it is hard to find $m$ such that $h(m)=y$24.
        
    - **Second Preimage Resistance:** Given $m$, it is hard to find a different $m^{\prime}$ where $h(m)=h(m^{\prime})$25.
        
    - **Collision Resistance:** It is hard to find _any_ two different messages $m$ and $m^{\prime}$ that hash to the same value26.
        
- **Collision Difficulty:** The difficulty of finding a collision is related to the birthday problem, requiring approximately $2^{\frac{n}{2}}$ operations, where $n$ is the bit length of the hash27272727.
    
    +1