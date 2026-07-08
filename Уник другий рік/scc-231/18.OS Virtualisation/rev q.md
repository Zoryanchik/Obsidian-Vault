![[Pasted image 20251231174052.png]]

|**Feature**|**Virtual Machines (VMs)**|**Containers**|
|---|---|---|
|**Portability**|**Lower.** Paravirtualization has "poor portability" (requires modified OS). Hardware-assisted is better, but VMs generally require moving full OS images.|**Higher.** Docker (mentioned in the slide) is noted for "reproducible development environments," making it easy to move software between dev and prod.|
|**Performance**|**Slower.** Even with hardware assistance, there is overhead from running a full Guest OS and trapping instructions to the hypervisor.|**Native/Fast.** They are "lightweight" and avoid the overhead of a hypervisor and Guest OS execution.|
|**Resource Usage**|**High (Resource-intensive).** You must run an "entire copy of an operating system" and all its services for _each_ VM.|**Low (Efficient).** They share the Host OS kernel. You don't need to duplicate the OS for every app.|
**2. Kernel Ownership and Process View:**

- **In a VM, who owns the kernel?** The **Guest OS** owns the kernel. (As seen in the "Virtualisation" diagram, each VM has its own "Guest OS" block).
    
- **In a container, who owns the kernel?** The **Host OS** owns the kernel. (The "Linux Container" diagram shows all containers sitting on top of a single "Host OS").
    
- **How do containers achieve a unique view of the process tree?** They use **Namespaces**.
    
    - _Evidence:_ In the bottom-right corner of the second slide, inside the Host OS block, you can see **"Namespace"** listed alongside "CGroup". Namespaces are the Linux feature that isolates resources (like the process tree) so a container thinks it is the only thing running.

![[Pasted image 20251231174337.png]]### Recap Questions (2)

**1. Select which technology offers the best performance in the following scenarios:**

- **Run multiple instances of a web server with minimal overhead:** **Answer: Containerisation.**
    
    - _Reasoning:_ The slide emphasizes that containers are "lightweight" and aim to achieve benefits "without the overhead" of running full OS copies for each instance.
        
- **Control the kernel configuration for a cloud application:** **Answer: Virtualisation.**
    
    - _Reasoning:_ Since containers share the Host OS kernel, they cannot modify it without affecting every other container. A VM has its own independent **Guest OS** (as shown in the diagrams), so you can configure its kernel however you like without impacting the host or other VMs.
        
- **Run a database service for a medical application storing important patient data:** **Answer: Virtualisation.**
    
    - _Reasoning:_ While not explicitly spelled out in terms of "security" on the slide, the architecture implies it. Virtualization provides stronger hardware-level isolation (e.g., **Ring 0** isolation and **Root mode** described in the first slide). Containers share the kernel (slide 2), meaning a kernel vulnerability could expose all data. For critical medical data, the stronger isolation of a VM is typically preferred.