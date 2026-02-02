![[Pasted image 20260202234103.png]]![[Pasted image 20260202234115.png]]![[Pasted image 20260202234130.png]]```

``` Python

import os  # Import os module for generating cryptographically secure random bytes
from cryptography.hazmat.primitives.ciphers import Cipher, algorithms, modes  # Import encryption components

def encrypt(key, plaintext):
    """
    Encrypts plaintext using AES encryption in CFB8 mode.
    
    Parameters:
        key: 256-bit (32 bytes) encryption key
        plaintext: Data to encrypt (in bytes)
    
    Returns:
        iv: Initialization Vector used for encryption
        ciphertext: Encrypted data
    """
    
    # Generate a random 128-bit (16 bytes) Initialization Vector (IV)
    # IV ensures that encrypting the same plaintext twice produces different ciphertexts
    # This prevents pattern analysis attacks
    iv = os.urandom(16)
    
    # Create an AES cipher object with the provided key and CFB8 mode
    # AES (Advanced Encryption Standard) is a symmetric encryption algorithm
    # CFB8 (Cipher Feedback 8-bit) mode operates on 8-bit segments
    # This mode turns block cipher into stream cipher, allowing encryption of any length data
    cipher = Cipher(algorithms.AES(key), modes.CFB8(iv))
    
    # Create an encryptor object from the cipher
    # This object will perform the actual encryption operation
    encryptor = cipher.encryptor()
    
    # Encrypt the plaintext:
    # - update() processes the plaintext and returns encrypted bytes
    # - finalize() completes the encryption and returns any remaining bytes
    # - Both are concatenated to form complete ciphertext
    ciphertext = encryptor.update(plaintext) + encryptor.finalize()
    
    # Return both IV and ciphertext
    # IV must be stored/transmitted with ciphertext for decryption
    # IV doesn't need to be secret, but must be unique for each encryption
    return iv, ciphertext

def decrypt(key, ciphertext, iv):
    """
    Decrypts ciphertext using AES decryption in CFB8 mode.
    
    Parameters:
        key: Same 256-bit (32 bytes) encryption key used for encryption
        ciphertext: Encrypted data to decrypt
        iv: Same Initialization Vector used during encryption
    
    Returns:
        plaintext: Decrypted data (in bytes)
    """
    
    # Create an AES cipher object with the SAME key and IV used for encryption
    # Using the same key and IV is critical for successful decryption
    cipher = Cipher(algorithms.AES(key), modes.CFB8(iv))
    
    # Create a decryptor object from the cipher
    # This object will perform the actual decryption operation
    decryptor = cipher.decryptor()
    
    # Decrypt the ciphertext:
    # - update() processes the ciphertext and returns decrypted bytes
    # - finalize() completes the decryption and returns any remaining bytes
    # - Both are concatenated to form complete plaintext
    plaintext = decryptor.update(ciphertext) + decryptor.finalize()
    
    # Return the decrypted plaintext
    return plaintext

# Main program execution block
# Code here only runs when script is executed directly (not when imported as module)
if __name__ == "__main__":
    
    # ============ STEP 1: KEY GENERATION ============
    # Generate a random 256-bit (32 bytes) AES encryption key
    # AES supports key sizes of 128, 192, or 256 bits
    # 256-bit provides the highest security level
    # os.urandom() generates crypto

```
```
