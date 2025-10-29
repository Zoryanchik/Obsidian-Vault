### ![[Pasted image 20251029190717.png]]**a. Identify classes, attributes, operations, and relationships**

#### **Classes:**

1. **Contact**
    
2. **Address**
    
3. **PhoneNumber**
    
4. **Email**
    
5. **ContactBook**
    

---

#### **Attributes:**

**Contact**

- contactID
    
- firstName
    
- lastName
    
- birthday
    

**Address**

- street
    
- city
    
- state
    
- postalCode
    
- country
    

**PhoneNumber**

- type (e.g., mobile, home, work)
    
- number
    

**Email**

- type (e.g., personal, work)
    
- emailAddress
    

**ContactBook**

- name
    
- owner
    

---

#### **Operations (Methods):**

**Contact**

- addPhoneNumber()
    
- addEmail()
    
- addAddress()
    
- updateContact()
    
- deleteContact()
    

**ContactBook**

- addContact()
    
- removeContact()
    
- searchContact()
    
- listContacts()
    

---

#### **Relationships:**

- **ContactBook** _contains_ many **Contacts** → (1..*) composition
    
- **Contact** _has_ many **PhoneNumbers** → (1..*) aggregation
    
- **Contact** _has_ many **Emails** → (1..*) aggregation
    
- **Contact** _has one or more_ **Addresses** → (1..*) aggregation

![[Pasted image 20251029191046.png]]