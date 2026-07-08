![[Pasted image 20251013192920.png]]![[Pasted image 20251013193159.png]]![[Pasted image 20251013193210.png]]### 👩‍🦳 **Stakeholder 1: Mary**

- **Requirement 1 (F):**  
    The system **shall notify Mary when any food item in the fridge is about to expire**.
    
- **Requirement 2 (NF):**  
    The system **shall ensure that Mary’s personal and medical data is encrypted during storage and transmission**.
    

---

### 🧓 **Stakeholder 2: Age Concern representative (AC)**

- **Requirement 1 (F):**  
    The system **shall provide a simple visual interface that allows Mary to check her daily food and fluid intake**.
    
- **Requirement 2 (NF):**  
    The system **shall operate reliably with minimal manual input from the user** to support elderly users with limited technical ability.
    

---

### 🏛️ **Stakeholder 3: Government Health Committee (GHC)**

- **Requirement 1 (F):**  
    The system **shall send weekly health reports to Mary’s GP in compliance with NHS data exchange standards**.
    
- **Requirement 2 (NF):**  
    The system **shall comply with GDPR and NHS data privacy regulations when processing personal data**.
    

---

### 👨‍💻 **Stakeholder 4: System Developer (SD)**

- **Requirement 1 (F):**  
    The system **shall use existing smart home communication protocols (e.g., Wi-Fi, Bluetooth) for integration with other home devices**.
    
- **Requirement 2 (NF):**  
    The system **shall minimize development and maintenance costs by using commercially available components**.
    

---

## ⚔️ Step 3: Identify Possible Conflicts

|Conflict|Stakeholders Involved|Description|Possible Resolution|
|---|---|---|---|
|Data sharing vs Privacy|Mary / GHC|Mary wants strong privacy, while GHC needs to send medical data to GP|Encrypt health data before sending; share only necessary information|
|Simplicity vs Compliance|AC / GHC|AC wants a simple system for Mary, but GHC requires compliance with complex data regulations|Automate compliance in background; hide complexity from user|
|Cost vs Security|SD / Mary|Developer wants low-cost components, but Mary wants strong data security|Choose cost-effective components that still support encryption standards|

---

## 🧠 Step 4: Final Non-Conflicting (Revised) Requirements

1. The system **shall notify Mary when any food item is near expiry.**
    
2. The system **shall track and report Mary’s food and liquid intake to her GP using encrypted communication.**
    
3. The system **shall use a simple, easy-to-read display for Mary’s daily intake summary.**
    
4. The system **shall comply with NHS and GDPR data protection standards.**
    
5. The system **shall integrate with standard smart home communication protocols.**
    
6. The system **shall be cost-effective and require minimal user interaction.**