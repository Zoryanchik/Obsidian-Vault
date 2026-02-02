![[Pasted image 20260202181216.png]]![[Pasted image 20260202181224.png]]![[Pasted image 20260202181303.png]]StreaM Cypher = each bit byte is 
![[Pasted image 20260202181624.png]]
![[Pasted image 20260202181734.png]]![[Pasted image 20260202181849.png]]

|**Feature**|**Details**|
|---|---|
|**Input Block Size**|Operates on 16 bytes of input at a time.|
|**Architecture Type**|Uses a Substitution-Permutation Network (SPN).|
|**Supported Key Sizes**|Supports key lengths of 128, 192, and 256 bits.|
|**Round Operations**|1. Byte substitution<br><br>  <br><br>2. Shift rows<br><br>  <br><br>3. Mix columns<br><br>  <br><br>4. Add round key ($\oplus k_i$)|
|**Key Management**|A round key $k_i$ is derived from the main secret key $k$.|
|**Decryption**|Performed by executing the encryption steps in the reverse order.|
|**Performance**|Described as "very fast".|

![[Pasted image 20260202182527.png]]![[Pasted image 20260202182533.png]]![[Pasted image 20260202182635.png]]![[Pasted image 20260202182641.png]]![[Pasted image 20260202182648.png]]![[Pasted image 20260202182653.png]]