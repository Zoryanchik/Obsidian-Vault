Here are the summary notes from your lecture slides, organized by topic.

---

### 1. 🎯 The Core Problem: Names vs. Addresses

- **Humans prefer human-readable names** (hostnames), like `google.co.uk`.
    
- **Computers (machines) prefer IP addresses** to identify hosts and routers (e.g., `128.163.140.244` or 128-bit IPv6 addresses).
    
- **DNS (Domain Name System)** is the service that maps between these names and IP addresses.
    
- Domain names are **hierarchical**, forming a tree structure (e.g., `comp.lancs.ac.uk` is a subdomain of `lancs.ac.uk`).
    

### 2. 🏛️ DNS Design and Hierarchy

DNS is a massive, **distributed, hierarchical database**. A single, centralized database would not work because it would:

- Be a **single point of failure**.
    
- Not be **scalable** to handle all traffic.
    
- Be too difficult to **maintain**.
    

The hierarchy consists of three main types of servers:

- **Root DNS Servers:** 13 logical servers (replicated many times worldwide) that are the starting point for all lookups.
    
- **Top-Level Domain (TLD) Servers:** Responsible for top-level domains like `.com`, `.org`, `.net`, and country codes like `.uk` or `.fr`. For example, Network Solutions manages the `.com` TLD.
    
- **Authoritative DNS Servers:** The organization's own server that holds the actual, definitive records (hostname-to-IP mappings) for its domains.
    

A fourth type, the **Local DNS Server**, is not part of the hierarchy. It's the server your ISP or university provides and acts as a **proxy**, receiving your initial query and **caching** the results.

### 3. ⚙️ How DNS Works: Resolution and Caching

#### Name Resolution

There are two main methods for looking up a name:

1. **Iterative Query:** (This is the standard process)
    
    - The local server asks the Root server. The Root server replies, "I don't know, but ask the `.com` TLD server".
        
    - The local server asks the `.com` TLD server. The TLD server replies, "I don't know, but ask the `amazon.com` authoritative server".
        
    - The local server asks the `amazon.com` authoritative server, which finally replies with the IP address for `www.amazon.com`.
        
2. **Recursive Query:**
    
    - The local server asks an upstream server (e.g., the Root) to find the _entire_ answer and return it.
        
    - This puts a heavy processing load on the contacted server, so it's less common at the upper levels.
        

#### Caching

- To improve efficiency, when a DNS server learns a mapping, it **caches** it.
    
- **TTL (Time-To-Live)**: Each record has a TTL value (set by the authoritative server) that tells the cache how long to store the record before it expires and must be looked up again.
    
- Caching greatly reduces the traffic to the Root servers , but it means records can be **out-of-date** until the TTL expires.
    

---

### 4. 📋 DNS Resource Records (RRs)

DNS servers store data in **Resource Records (RRs)**. The standard format is: `(name, value, type, ttl)`.

Here are the essential types:

- **type=A**
    
    - **Name:** Hostname (e.g., `www.example.com`).
        
    - **Value:** IPv4 address.
        
- **type=NS** (Name Server)
    
    - **Name:** Domain (e.g., `example.com`).
        
    - **Value:** Hostname of the **authoritative name server** for that domain.
        
- **type=CNAME** (Canonical Name)
    
    - **Name:** An alias (e.g., `www.lancaster.ac.uk`).
        
    - **Value:** The "real" or canonical name (e.g., `www.lancs.ac.uk`).
        
- **type=MX** (Mail Exchange)
    
    - **Value:** The name of the **mail server** that handles email for the `name`.
        

### 5. 🚀 How to Set Up a New Domain

This is a two-part process:

1. **At the DNS Registrar (e.g., Network Solutions):**
    
    - You **register your domain name** (e.g., `networkutopia.com`).
        
    - You provide the registrar with the names and IP addresses of your **authoritative name servers**.
        
    - The registrar then inserts an **NS record** (to delegate your domain) and an **A record** (to find your name server) into the TLD server (e.g., the `.com` server).
        
2. **On Your Own Authoritative Server:**
    
    - You set up your server at its IP (e.g., `212.212.212.1`).
        
    - You create the specific records for your services, such as:
        
        - An **A record** for `www.networkutopia.com` to point to your web server.
            
        - An **MX record** for `networkutopia.com` to point to your mail server.
            

---

### 6. ℹ️ Other Concepts

- **HTTP/1.1 vs. HTTP/2:** HTTP/1.1 suffered from **Head-of-Line (HOL) blocking**, where a large object (like a video) would block smaller objects from being delivered. HTTP/2 solves this by dividing all objects into **frames** and **interleaving** them, so small objects can be delivered quickly without waiting.
    
- **DNS Importance:** DNS is on the **critical path** for almost all communication. If DNS is slow or unreliable, most internet services (web, email, apps) will break or be severely delayed.
    
- **`dig` command:** A utility to query DNS. `dig +trace example.com` is useful to see the full iterative query process from the root servers down.