![[Pasted image 20260111205958.png]]In this **Proxy Pattern** diagram, aggregation is used to show that the **Proxy** controls a **RealSubject** without owning its entire life cycle.![[Pasted image 20260111213703.png]]
![[Pasted image 20260111224328.png]]![[Pasted image 20260111224904.png]]![[Pasted image 20260112002002.png]]A Proxy is a **surrogate or placeholder** that sits between a Client and the Real Object to control access.

- **Controlled Access:** The client thinks it is talking to the real object, but it is actually talking to the Proxy.
    
- **Forwarding Requests:** The Proxy class **stores an instance** of the `RealSubject`. When you call a method on the Proxy, it simply forwards that request to the real instance: `realSubject.request()`.
    
- **Alternative Design (Lazy Loading):** In your contact book example, the `ContactBookProxy` is used to save memory. It doesn't create the heavy `ContactBookImpl` object until someone actually tries to search for or get a contact.

![[Pasted image 20260112002310.png]]![[Pasted image 20260112004103.png]]![[Pasted image 20260112004111.png]]![[Pasted image 20260112004119.png]]![[Pasted image 20260112004219.png]]![[Pasted image 20260112004342.png]]![[Pasted image 20260112004352.png]]![[Pasted image 20260112005521.png]]![[Pasted image 20260112005728.png]]