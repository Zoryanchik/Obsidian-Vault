![[Pasted image 20251104021330.png]]- **Requesting host → Local DNS server**
    
    - The host `cis.poly.edu` asks its local DNS (`dns.poly.edu`):  
        “What is the IP of `gaia.cs.umass.edu`?”
        
- **Local DNS → Root DNS server**
    
    - The local DNS doesn’t know, so it asks a **root DNS server**.
        
- **Root DNS → Local DNS**
    
    - The root server replies:  
        “I don’t know `gaia.cs.umass.edu`, but ask the **.edu TLD DNS server**.”
        
- **Local DNS → TLD (.edu) DNS server**
    
    - The local DNS now queries the **TLD DNS** for `.edu`.
        
- **TLD DNS → Local DNS**
    
    - The `.edu` server responds:  
        “I don’t know `gaia.cs.umass.edu`, but the **authoritative server for cs.umass.edu** can tell you.”
        
- **Local DNS → Authoritative DNS server**
    
    - The local DNS asks the **authoritative DNS** (`dns.cs.umass.edu`):  
        “What’s the IP for `gaia.cs.umass.edu`?”
        
- **Authoritative DNS → Local DNS**
    
    - The authoritative DNS replies:  
        “The IP for `gaia.cs.umass.edu` is **128.119.40.12**” (example).
        
- **Local DNS → Requesting host**
    
    - Finally, the local DNS returns that IP address to the original host `cis.poly.edu`
- ![[Pasted image 20251104021851.png]]A **recursive query** is when your **DNS resolver (usually your ISP’s or Google’s DNS)** does **all the work for you** — it finds the final IP address **on your behalf** and then returns the final answer.
![[Pasted image 20251104022230.png]]