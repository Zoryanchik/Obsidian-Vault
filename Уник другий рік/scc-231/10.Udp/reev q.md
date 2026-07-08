![[Pasted image 20251109212108.png]]his question is about **UDP demultiplexing** — how incoming UDP packets are delivered to sockets.

Here’s the key idea 👇

---

### 🧩 Situation:

- Host C has **one UDP socket**, bound to **port 6789**.
    
- Both Host A and Host B send UDP packets to Host C’s port 6789.
    

---

### 🧠 What happens:

✅ **Both UDP segments go to the same socket** on Host C,  
because **UDP demultiplexing** uses **only the destination port number** (unlike TCP, which uses source & destination IP/port pairs).

So:

`Host A → Host C: port 6789   Host B → Host C: port 6789`  

➡ Both are delivered to the same UDP socket.

---

### 💡 How Host C knows who sent what:

Each UDP datagram carries:

- **source IP address**, and
    
- **source port number**
    

When Host C receives the packet, the socket API (e.g., `recvfrom()` in C or Python) provides this info.

Example (Python):

`data, addr = sock.recvfrom(1024) print("Received from:", addr)`

Output might be:

`Received from: ('192.168.1.10', 4567) Received from: ('192.168.1.20', 9876)`

So even though both packets go to the same socket,  
the **application** can distinguish them by checking `addr` (the sender’s IP and port).

---

✅ **Summary:**

| Concept                   | UDP Behavior                          |
| ------------------------- | ------------------------------------- |
| Socket identified by      | Destination port only                 |
| Multiple senders          | Delivered to same socket              |
| How to tell senders apart | Source IP & port in the packet header |
![[Pasted image 20251109212141.png]]### Given:

Three 16-bit words:

`0101001101100110   0111010011010100   0000110111000001`

---

## 🧩 Step 1: Add the three binary words

Let’s add them using normal binary addition, but with **wrap-around carry** (as in 1’s complement arithmetic).

   `0101001101100110 +  0111010011010100 -------------------    1100011100111010   (no carry yet)`

Now add the third one:

   `1100011100111010 +  0000110111000001 -------------------    1101010101111011   (no carry beyond 16 bits)`

✅ **Sum (before complement):**  
`1101010101111011`

---

## 🧮 Step 2: Take the 1’s complement

Invert all bits (0→1, 1→0):

`0010101010000100`

✅ **Checksum = 0010101010000100**

---

## 💡 Step 3: Why UDP offers a checksum

UDP is connectionless — it doesn’t guarantee reliable delivery.  
So the **checksum** helps detect:

- Transmission errors (bit flips)
    
- Corrupted headers or data
    

If the receiver’s computed checksum **doesn’t match**, the packet is discarded.

---

## 🧠 Step 4: How receiver detects errors (1’s complement)

The receiver adds:

`All received 16-bit words + checksum`

If the **result = all 1’s (1111111111111111)** → ✅ no error  
Otherwise → ❌ error detected

---

## ⚙️ Step 5: Detecting a single-bit flip

If **one bit** changes during transmission (e.g., 0 → 1),  
the binary sum will no longer produce all 1’s.  
Thus, the checksum comparison will **fail**, and the receiver knows the data is corrupted.

---

✅ **Summary**

|Concept|Explanation|
|---|---|
|**Sum**|`1101010101111011`|
|**1’s complement (checksum)**|`0010101010000100`|
|**UDP checksum purpose**|Detect bit errors in data|
|**Error detection**|Sum + checksum = all 1’s → OK|
|**Single-bit flip**|Causes mismatch → detected|