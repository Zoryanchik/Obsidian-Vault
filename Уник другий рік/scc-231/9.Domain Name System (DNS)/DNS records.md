![[Pasted image 20251104022422.png]]Certainly! Based on that slide, here is a practical summary of what you need to **do** with each DNS record type when configuring a domain.

### 🅰️ type=A (Address Record)

- **What to do:** Use this to point a hostname (like `www.yourdomain.com` or the root `yourdomain.com`) directly to your server's **IPv4 address** (e.g., `192.0.2.1`).
    
- **In short:** This is the most basic record. It connects a name to a server's numeric IP address.
    

### 🧭 type=NS (Name Server Record)

- **What to do:** Use this to tell the internet which servers are in charge of (authoritative for) all the DNS settings for your domain.
    
- **In short:** You usually set these at your **domain registrar** (where you bought the domain) to point to your **DNS host** (like your web hosting provider or a service like Cloudflare).
    

### ➡️ type=CNAME (Canonical Name Record)

- **What to do:** Use this to make one domain name (an "alias," like `shop.yourdomain.com`) point to _another, different_ **domain name** (the "canonical" or real name, like `your-store.shopify.com`).
    
- **In short:** This is for pointing a subdomain to an external service or another part of your site that has a different name. It links a name _to another name_, not an IP address.
    

### ✉️ type=MX (Mail Exchange Record)

- **What to do:** Use this to specify which servers should receive **email** for your domain. The value will be the hostname of your mail provider (e.g., `mail.google.com`).
    
- **In short:** This record is essential for making your email (like `you@yourdomain.com`) work.
![[Pasted image 20251104022822.png]]![[Pasted image 20251104023043.png]]![[Pasted image 20251104023314.png]]Here is a step-by-step summary of what you need to do to set up a new domain, based on that slide.

This process is broken into two main parts:

1. **Registering:** Telling the _world's_ DNS system where to find your domain's settings.
    
2. **Configuring:** Setting up your _own_ server to answer questions about your domain.
    

---

### 1. At Your Domain Registrar (e.g., Network Solutions, GoDaddy)

- **Buy (register) your domain name** (e.g., `networkutopia.com`).
    
- **Tell your registrar the hostnames** of your **authoritative name servers**. These are the servers that will hold all your specific records (like A, MX, etc.). Your web host or DNS provider (like Cloudflare) will give you these names (e.g., `dns1.networkutopia.com` or `ns1.yourhost.com`).
    
- **Provide the IP address for your name server** (e.g., `212.212.212.1`). This is often called a "glue record" and is necessary so the internet can find your name server in the first place.
    

**What this does:** The registrar tells the central `.com` DNS servers (the TLD servers) to add:

- An **NS record** to delegate `networkutopia.com` to your server (`dns1.networkutopia.com`).
    
- An **A record** (glue record) to map your server's _name_ (`dns1.networkutopia.com`) to its _IP address_ (`212.212.212.1`).
    

---

### 2. On Your Authoritative Name Server (e.g., Your Web Host's cPanel, Cloudflare Dashboard)

Now that the world knows _where_ to look, you must set up that server to provide the answers.

- **Log in to your server's DNS settings** (the one with the IP `212.212.212.1`).
    
- **Create an A record** to point your website hostname (like `www.networkutopia.com`) to your **web server's IP address**. (This might be the same IP, or a different one).
    
- **Create an MX record** to point your domain's email (e.g., for `user@networkutopia.com`) to the **hostname of your mail server** (e.g., `mail.yourprovider.com`).
    

Would you like to know how to check the live DNS records for an existing domain?

![[Pasted image 20251104024445.png]]## 🧩 **Breaking down your examples:**

### 1️⃣ `dig -4 +trace example.com`

- **`-4`** → forces IPv4 only (no IPv6).
    
- **`+trace`** → shows the **entire DNS resolution path**, starting from **root servers** down to the **authoritative server**.  
    You’ll see how the query “travels” step by step:
    
    `. (root)  → .com (TLD)    → example.com (authoritative)`
    ### 2️⃣ `dig www.lancaster.ac.uk CNAME`

- This asks for the **CNAME record** (Canonical Name).
    
- CNAME tells you if a domain is **an alias** for another name.  
    Example output:
    
    `www.lancaster.ac.uk.  CNAME  web-lb.lancaster.ac.uk.`
    
    Meaning → `www.lancaster.ac.uk` is just another name for `web-lb.lancaster.ac.uk`.
    

---

### 3️⃣ `dig lancs.ac.uk MX`

- Asks for **MX (Mail eXchanger)** records — i.e. which mail servers handle email for that domain.  
    Example:
    
    `lancs.ac.uk.  MX  10 mail.lancs.ac.uk.`
    
    Meaning → mail for `@lancs.ac.uk` should go to **mail.lancs.ac.uk**.
    

---

### 4️⃣ `dig www.google.com`

- Queries the standard **A record** (IPv4 addresses).
    
- Google usually returns **multiple IPs** — this is **load balancing**:
    
    `www.google.com.  A  142.250.180.68 www.google.com.  A  142.250.180.100 ...`
    
    The order of these IPs can **change each time**, spreading traffic across multiple servers.