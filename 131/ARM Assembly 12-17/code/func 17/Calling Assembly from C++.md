![[Pasted image 20250228230453.png]]![[Pasted image 20250228231139.png]]
![[Pasted image 20250228231436.png]]
![[Pasted image 20250228231526.png]]
![[Pasted image 20250228231551.png]]
![[Pasted image 20250228234921.png]]
![[Pasted image 20250228235005.png]]
деклариривает что в другом файле есть функий eth_mult и мы можем использовать 
![[Pasted image 20250228235053.png]]
И тут уже забирает наш r0 из ассембли (где прошла функция) и принтит
![[Pasted image 20250228234735.png]]
pc lr return back
When a function is called using the **BL** (Branch with Link) instruction, the processor automatically saves the **return address** (the instruction after the call) into the **LR register**.
![[Pasted image 20250303163138.png]]
