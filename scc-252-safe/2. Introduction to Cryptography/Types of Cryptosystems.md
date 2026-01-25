![[Pasted image 20260118203816.png]]![[Pasted image 20260118204048.png]]![[Pasted image 20260118204058.png]]- **$P$ (Plaintext):** This is simply your **original message**. It's the readable letter you want to send (e.g., "Hello")1.
    
- **$C$ (Ciphertext):** This is the **scrambled message**. If someone looks at the letter while it's locked in the box or encrypted, they just see gibberish2.
    
- **$K$ (Key Space):** These are all the possible **keys** or passwords available to lock and unlock the box. The security depends on there being so many possible keys that a bad guy can't just guess the right one3.#

- **$Enc$ (Encryption Function):** This is the action of **locking the box**. You take your message ($P$) and use a specific key ($ek$) to turn it into scrambled code ($C$)4.
    
- **$Dec$ (Decryption Function):** This is the action of **unlocking the box**. You take the scrambled code ($C$) and use a specific key ($dk$) to turn it back into the original message ($P$)5.
    

### 3. The "Golden Rule" (The Formula at the Bottom)

The complicated-looking math at the bottom ($\forall ek \in K \dots$) is essentially a guarantee that the system actually works. It translates to:

> **"For every locking key, there must be a matching unlocking key. If you lock a message and then unlock it with the correct key, you MUST get the exact same original message back."** 6


![[Pasted image 20260118204434.png]]
A cryptographic key is ==a secret piece of data (like a long string of numbers/letters) used with an algorithm to scramble (encrypt) and unscramble (decrypt) digital information, turning readable text (plaintext) into unreadable code (ciphertext) and back again, with the security of the system depending on the key's randomness and secrecy, commonly using [symmetric](https://www.google.com/search?q=symmetric&oq=cryptographic+key&gs_lcrp=EgZjaHJvbWUyBggAEEUYOTIHCAEQABiABDIHCAIQABiABDIICAMQABgWGB4yCAgEEAAYFhgeMggIBRAAGBYYHjIICAYQABgWGB4yCAgHEAAYFhgeMggICBAAGBYYHjIICAkQABgWGB7SAQg0NjY5ajBqNKgCALACAQ&sourceid=chrome&ie=UTF-8&ved=2ahUKEwj74uTS35WSAxUJW0EAHUy_A4UQgK4QegYIAAgAEAY) (one key) or [asymmetric](https://www.google.com/search?q=asymmetric&oq=cryptographic+key&gs_lcrp=EgZjaHJvbWUyBggAEEUYOTIHCAEQABiABDIHCAIQABiABDIICAMQABgWGB4yCAgEEAAYFhgeMggIBRAAGBYYHjIICAYQABgWGB4yCAgHEAAYFhgeMggICBAAGBYYHjIICAkQABgWGB7SAQg0NjY5ajBqNKgCALACAQ&sourceid=chrome&ie=UTF-8&ved=2ahUKEwj74uTS35WSAxUJW0EAHUy_A4UQgK4QegYIAAgAEAc) (public/private pair) methods==.

![[Pasted image 20260118204559.png]]
![[Pasted image 20260118204616.png]]![[Pasted image 20260118204706.png]]![[Pasted image 20260118204816.png]]