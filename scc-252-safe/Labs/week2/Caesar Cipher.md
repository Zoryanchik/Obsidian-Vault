```Python
def createSubstitutionTables(shiftNumber):

    # Build lookup maps for a Caesar cipher using the provided shift.

    #we use dictionaries because they provide O(1) average time complexity for lookups.

    plaintextToCiphertext = {} # here we are saving

    ciphertextToPlaintext = {}

  

    for i in range(26):

        # Work through the alphabet from 'a' to 'z'.

        plaintextChar = chr(ord('a') + i)

  

        # Shift the character by shiftNumber with wrap-around using modulo 26.

        ciphertextChar = chr(ord('a') + (i + shiftNumber) % 26)

        #we % 26 to ensure that if we go past 'z', we wrap around back to 'a'.

  

        # Populate both forward (plain->cipher) and reverse (cipher->plain) maps.

        plaintextToCiphertext[plaintextChar] = ciphertextChar

        ciphertextToPlaintext[ciphertextChar] = plaintextChar

  

def encrypt(plaintext, plaintextToCiphertext):

    cipher = ""

  

    # Go through each character in the message

    for char in plaintext:

        if char in plaintextToCiphertext:

            # If it's a letter, encrypt it

            cipher += plaintextToCiphertext[char] #this will get the corresponding cipher character from the map

        else:

            # If it's not a letter (space, etc.), keep it as is

            cipher += char

    return cipher

  

def decrypt(ciphertext, ciphertextToPlaintext):

    plain = ""

  

    # Go through each character in the message

    for char in ciphertext:

        if char in ciphertextToPlaintext:

            # If it's a letter, decrypt it

            plain += ciphertextToPlaintext[char] #this will get the corresponding plain character from the map

        else:

            # If it's not a letter (space, etc.), keep it as is

            plain += char

    return plain

  

if __name__ == "__main__":

    shift = 3  # Example shift value for Caesar cipher

    plaintextToCiphertext, ciphertextToPlaintext = createSubstitutionTables(shift)

  

    message = "hello world"

    encryptedMessage = encrypt(message, plaintextToCiphertext)

    print("Encrypted:", encryptedMessage)

  

    decryptedMessage = decrypt(encryptedMessage, ciphertextToPlaintext)

    print("Decrypted:", decryptedMessage)s
```


**Exercise 2 Answer:** The Caesar cipher is not secure because there are only 25 possible shifts (1-25). An attacker can simply try all 25 possibilities in seconds and see which one makes sense. This is called a "brute force attack.

![[Pasted image 20260126192314.png]]


![[Pasted image 20260126200522.png]]
```Python
# Task: Include any required modules here

from unittest import result

  

def createSubstitutionTables(key):

    # The key is the ciphertext alphabet

    # "ESKMXRBPVHDTNFZAYQWILCOUGJ" from Table 2

    plaintextToCiphertext = {}

    ciphertextToPlaintext = {}

    # Map each letter A-Z to the corresponding letter in the key

    for i in range(26):

        plainLetter = chr(ord('A') + i)

        cipherLetter = key[i]

        plaintextToCiphertext[plainLetter] = cipherLetter

        ciphertextToPlaintext[cipherLetter] = plainLetter

    return (plaintextToCiphertext, ciphertextToPlaintext)

  

def encrypt(plaintext, plaintextToCiphertext):

    cipher = ""

    for char in plaintext:

        if char in plaintextToCiphertext:

            cipher += plaintextToCiphertext[char]

        else:

            cipher += char

    return cipher

  
  

def decrypt(ciphertext, ciphertextToPlaintext):

    result = ""

    for char in ciphertext:

        if char in ciphertextToPlaintext:

            result += ciphertextToPlaintext[char]

        else:

            result += char

    return result

  

if __name__ == "__main__":

    # Create the substitution tables using the key from Table 2

    # A B C D E F G H I J K L M N O P Q R S T U V W X Y Z

    # E S M X K R B P V H D T N F Z A Y Q W I L C O U G J

    key = "ESKMXRBPVHDTNFZAYQWILCOUGJ"

    plainToCipher, cipherToPlain = createSubstitutionTables(key)

    # Define a plaintext to encrypt

    message = "SUBSTITUTION"

    # Encrypt the plaintext and print the ciphertext

    encrypted = encrypt(message, plainToCipher)

    print("Plaintext:", message)

    print("Ciphertext:", encrypted)

    # Decrypt the ciphertext and print the plaintext

    decrypted = decrypt(encrypted, cipherToPlain)

    print("Decrypted:", decrypted)
```

![[Pasted image 20260126221221.png]]
![[Pasted image 20260126221208.png]]