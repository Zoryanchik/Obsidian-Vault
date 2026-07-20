![[Pasted image 20260720184152.png]]![[Pasted image 20260720185243.png]]
### Key Components

- **Merchant:** The business selling the goods or services.
    
- **PSP (Payment Service Provider):** A third-party company that provides merchants with the tools necessary to accept electronic payments. In this diagram, the PSP encompasses two main elements:
    
    - **Payment Gateway:** The technology that securely captures the customer's payment data at checkout and transmits it. Think of it as a digital point-of-sale (POS) terminal.
        
    - **Acquiring Bank:** The bank that holds the merchant's business account and receives the funds on the merchant's behalf.
        
- **Processing Center:** Facilities or systems that act as intermediaries, securely routing the transaction data between the payment gateway, card networks, and banks.
    
- **Card Network:** The company that manages the card brand (e.g., Visa, Mastercard, American Express). They act as the central switchboard, connecting the merchant's bank to the customer's bank.
    
- **Issuer Bank:** The bank that issued the credit or debit card to the customer. This bank holds the customer's funds and is responsible for approving or declining the transaction.
    

### The Transaction Flow

Following the arrows in the diagram, here is how the data moves:

1. **Checkout:** The **Merchant** sends the customer's payment information to the **Payment Gateway** (within the PSP).
    
2. **Acquiring Side Processing:** The Payment Gateway, working in tandem with the **Acquiring Bank**, securely forwards the transaction request to a **Processing Center**.
    
3. **Routing to the Network:** The Processing Center sends the transaction data to the appropriate **Card Network** (based on whether the customer used a Visa, Mastercard, etc.).
    
4. **Routing to the Issuer:** The Card Network routes the transaction through another **Processing Center** to reach the specific **Issuer Bank**.
    
5. **Authorization:** The **Issuer Bank** receives the request, checks if the customer has sufficient funds and ensures the transaction isn't fraudulent. It then sends an "approved" or "declined" message all the way back through this exact same chain to the merchant so the sale can be completed.