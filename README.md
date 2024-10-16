# Kriptografi_PlayfairCipher

#### Nama : Vivie Zuliani Eriksari
#### NIM : 312210475
#### Kelas : TI.22.A5

---
### TUGAS :

![Screenshot 2024-10-16 134301](https://github.com/user-attachments/assets/aec50503-251a-4878-8e6e-e6538aaf5a83)

### JAWABAN :
> Code Kriptografi Playfair.py
```
import numpy as np

# Generate the Playfair matrix
def generate_playfair_matrix(key):
    key = ''.join(sorted(set(key), key=key.index)).replace('J', 'I')  # Remove duplicates and replace J with I
    alphabet = "ABCDEFGHIKLMNOPQRSTUVWXYZ"
    matrix = key + ''.join([c for c in alphabet if c not in key])
    return np.array([list(matrix[i:i + 5]) for i in range(0, 25, 5)])

# Preprocess the text (for both encryption and decryption)
def preprocess_text(text):
    text = text.replace('J', 'I').replace(' ', '').upper()
    processed_text = ''
    i = 0
    while i < len(text):
        processed_text += text[i]
        if i + 1 < len(text) and text[i] == text[i + 1]:
            processed_text += 'X'
        elif i + 1 < len(text):
            processed_text += text[i + 1]
            i += 1
        i += 1
    if len(processed_text) % 2 != 0:
        processed_text += 'X'
    return processed_text

# Find position of the character in the matrix
def find_position(matrix, char):
    pos = np.where(matrix == char)
    return pos[0][0], pos[1][0]

# Encrypt using Playfair Cipher
def playfair_encrypt(plaintext, key):
    matrix = generate_playfair_matrix(key)
    plaintext = preprocess_text(plaintext)
    ciphertext = ''
    
    for i in range(0, len(plaintext), 2):
        row1, col1 = find_position(matrix, plaintext[i])
        row2, col2 = find_position(matrix, plaintext[i + 1])
        
        if row1 == row2:
            ciphertext += matrix[row1, (col1 + 1) % 5]
            ciphertext += matrix[row2, (col2 + 1) % 5]
        elif col1 == col2:
            ciphertext += matrix[(row1 + 1) % 5, col1]
            ciphertext += matrix[(row2 + 1) % 5, col2]
        else:
            ciphertext += matrix[row1, col2]
            ciphertext += matrix[row2, col1]
    
    return ciphertext

# Decrypt using Playfair Cipher
def playfair_decrypt(ciphertext, key):
    matrix = generate_playfair_matrix(key)
    plaintext = ''
    
    for i in range(0, len(ciphertext), 2):
        row1, col1 = find_position(matrix, ciphertext[i])
        row2, col2 = find_position(matrix, ciphertext[i + 1])
        
        if row1 == row2:
            plaintext += matrix[row1, (col1 - 1) % 5]
            plaintext += matrix[row2, (col2 - 1) % 5]
        elif col1 == col2:
            plaintext += matrix[(row1 - 1) % 5, col1]
            plaintext += matrix[(row2 - 1) % 5, col2]
        else:
            plaintext += matrix[row1, col2]
            plaintext += matrix[row2, col1]
    
    return plaintext

# Main
key = "TEKNIKINFORMATIKA"
texts = [
    "GOOD BROOM SWEEP CLEAN",
    "REDWOOD NATIONAL STATE PARK",
    "JUNK FOOD AND HEALTH PROBLEMS"
]

print("Encryption and Decryption using Playfair Cipher with key:", key)
for text in texts:
    encrypted = playfair_encrypt(text, key)
    decrypted = playfair_decrypt(encrypted, key)
    
    print(f"Plaintext: {text}")
    print(f"Encrypted: {encrypted}")
    print(f"Decrypted: {decrypted}")
    print("----------")
```
  


### Output :

![Screenshot 2024-10-16 135811](https://github.com/user-attachments/assets/cd63fc4b-be41-4cda-9653-3d2997bde109)


![Screenshot 2024-10-16 135746](https://github.com/user-attachments/assets/1cc78658-59f8-4a9c-aebc-da7179f5da30)

![Screenshot 2024-10-16 135759](https://github.com/user-attachments/assets/54d68c6b-1703-4432-87a4-37c92f76f02d)





