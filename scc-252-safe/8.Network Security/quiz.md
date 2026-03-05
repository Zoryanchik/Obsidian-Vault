## 1. What does network security concern with?

Network security is the practice of protecting the integrity, confidentiality, and accessibility of computer networks and data. It involves both **hardware** (like firewalls) and **software** (like encryption) technologies.

The primary goal is to prevent unauthorized access, misuse, or theft. Think of it as the "perimeter defense" of your digital house—keeping the burglars out while making sure the residents can still get through the front door easily.

---

## 2. Common Network Types

Networks are generally categorized by their geographical scale:

- **PAN (Personal Area Network):** Very small range (usually within a room). Think of your phone connecting to your Bluetooth headphones.
    
- **LAN (Local Area Network):** Connects devices in a limited area like a home, office, or school. Usually high-speed and private.
    
- **WLAN (Wireless Local Area Network):** A LAN that uses wireless technology (Wi-Fi) instead of cables.
    
- **WAN (Wide Area Network):** Spans a large distance, like a city, country, or the entire globe. The **Internet** is the world's largest WAN.
    

---

## 3. The OSI Model (7 Layers)

The OSI (Open Systems Interconnection) model is a conceptual framework used to understand how data moves from one device to another.

![OSI model 7 layers, создано искусственным интеллектом](https://encrypted-tbn3.gstatic.com/licensed-image?q=tbn:ANd9GcRJ8yR5geShpbKY1QWH6vIfApddL4itNgiq6KZfTe0Z2hCCMm01EkbHpNAoxvGdT67pUwejucBavnUDGpmQ4T559b8UPqruAGvo2SshT3UjQakQw1A)

Shutterstock

Открыть

|**Layer**|**Name**|**Function**|
|---|---|---|
|**7**|**Application**|Where the user interacts (HTTP, SMTP, FTP).|
|**6**|**Presentation**|Data formatting, encryption, and compression.|
|**5**|**Session**|Manages connections between applications.|
|**4**|**Transport**|End-to-end communication (TCP, UDP).|
|**3**|**Network**|Path determination and IP addressing (Routing).|
|**2**|**Data Link**|Physical addressing (MAC addresses).|
|**1**|**Physical**|Physical cables, bits, and voltages.|

---

## 4. The TCP/IP Model (4 Layers)

The TCP/IP model is the "real world" version of the OSI model, focusing on the protocols that actually run the internet.

1. **Application Layer:** Combines OSI layers 5, 6, and 7.
    
2. **Transport Layer:** Corresponds to OSI layer 4.
    
3. **Internet Layer:** Corresponds to OSI layer 3.
    
4. **Network Access Layer:** Combines OSI layers 1 and 2.
    

---

## 5. The "Weakest" Layer

From a security perspective, **Layer 7 (Application)** is often considered the weakest. This isn't because the protocols are poorly designed, but because it is the layer closest to the **human user**.

Most successful attacks (Phishing, SQL injection, Cross-site scripting) target the application layer or the people using it. As the saying goes: "There is no patch for human stupidity."

---

## 6. Where is the 'Packet' associated?

The term **Packet** is associated with **Layer 3 (Network Layer)**.

As data moves down the OSI stack, it changes names (this is called **encapsulation**):

- Layer 4: **Segment** (TCP) or **Datagram** (UDP)
    
- Layer 3: **Packet**
    
- Layer 2: **Frame**
    

---

## 7. The TCP Three-Way Handshake

Before two devices can exchange data via TCP, they must perform a "handshake" to ensure both sides are ready.

1. **SYN (Synchronize):** Client sends a packet to the server saying, "I'd like to talk."
    
2. **SYN-ACK (Synchronize-Acknowledge):** Server responds, "I received your request. I'm ready to talk too."
    
3. **ACK (Acknowledge):** Client says, "Great, I heard you. Let's start."
    

---

## 8. DoS vs. DDoS Attacks

These attacks aim to shut down a service by overwhelming it with traffic.

- **DoS (Denial of Service):** A single computer sends a flood of traffic to a target to crash it.
    
- **DDoS (Distributed Denial of Service):** The attacker uses a "botnet" (thousands of infected computers/IoT devices) to attack a target simultaneously. It’s much harder to block because the attack is coming from thousands of different IP addresses at once.