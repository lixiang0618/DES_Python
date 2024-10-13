# 🔐 **DES Encryption and Decryption Program**

## 🌐 Language Navigation
- [中文版本 (Chinese Version)](README.md)
- [English Version](README_EN.md)

> **Data Privacy and Information Security Course DES Algorithm Experiment, School of Information Management, Central China Normal University**  
> This project is a personal attempt to master the classic DES encryption algorithm. I take no responsibility for its use for other purposes. It is intended solely for academic exchange and learning. Data security enthusiasts and encryption technology learners are welcome to contribute and provide feedback.

---

## 📑 **Table of Contents**
- 🚀 [Project Overview](#project-overview)
- 🔍 [DES Principles](#des-principles)
  - ❓ [What is DES?](#what-is-des)
  - 🔐 [DES Encryption Process](#des-encryption-process)
- 🗂 [Project Structure](#project-structure)
- ✨ [Main Features](#main-features)
- 📦 [Installation and Usage](#installation-and-usage)
- 🛠 [Usage Examples](#usage-examples)
- ⚠️ [Notes](#notes)

---

## Project Overview
This project implements the **Data Encryption Standard (DES)** algorithm, a classic example of symmetric encryption used for secure data transmission. The program supports encryption and decryption of text, along with Base64 encoding and decoding to ensure encrypted data can be stored or transmitted effectively.

---

## DES Principles

### What is DES?
**DES (Data Encryption Standard)** is a symmetric-key encryption algorithm proposed by the U.S. National Institute of Standards and Technology (NIST) and widely used for encrypting sensitive data, such as in the financial sector. DES encrypts 64-bit plaintext using a 64-bit key, producing a 64-bit ciphertext.

**Encryption Type**: Symmetric encryption  
**Key Length**: 64 bits (with 8 bits used as parity bits)  
**Encryption Process**: 16 rounds of Feistel network iteration

### DES Encryption Process

1. **Initial Permutation (IP)**: The plaintext undergoes a bit-level transformation before encryption.
2. **Partitioning and Key Generation**: The 64-bit plaintext is divided into left (L) and right (R) sections, and 16 subkeys are generated.
3. **16 Rounds of Iteration**:
   - Expand the right section R to 48 bits.
   - XOR the data with the subkey.
   - Use S-box substitution to reduce the data back to 32 bits.
   - Swap the left and right sections.
4. **Inverse Initial Permutation (IP-1)**: The final 64-bit ciphertext is produced.

> **Diagram:**
>
> ```plaintext
> +-----------------+      +-------------------+      +-------------------+
> |   Plaintext In   | ---> | Initial Permutation | ---> |  16 Rounds of    |
> +-----------------+      +-------------------+      + Encryption         |
>                                                       |
> +-----------------+      +-------------------+      |
> | Inverse Initial | <--- |   Ciphertext Out   | <--- |
> | Permutation     |      +-------------------+      +-------------------+
> +-----------------+
> ```

---

## Project Structure
- `DES_BOX.py`: Contains constants used in the DES algorithm, such as initial permutation tables, S-boxes, and P-box.
- `main.py`: Core encryption and decryption logic, along with user interaction.

---

## Main Features

### 📝 File Handling
- **`read_file(filename)`**: Reads plaintext from a specified text file.
- **`write_file(message)`**: Writes encrypted ciphertext to the `ciphertext.txt` file.

### 🔐 Base64 Encoding and Decoding
- **`base64_encode(bit_string)`**: Converts a binary string into Base64 encoding for easy storage and transmission.
- **`base64_decode(encoded_string)`**: Reverts the Base64 encoding back to a binary string.

### 🔑 Key and Plaintext Processing
- **`process_key(key)`**: Processes the input key string to generate a 64-bit key.
- **`str_bit(message)`**: Converts a plaintext string to a binary bit string.
- **`divide(bits, bit)`**: Splits the binary stream into 64-bit segments for encryption.

### 🔒 DES Encryption and Decryption
- **`des_encrypt(bits, key)`**: Encrypts a 64-bit plaintext block using DES, returning the ciphertext.
- **`des_decrypt(bits, key)`**: Decrypts a 64-bit ciphertext block, returning the plaintext.
- **`all_des_encrypt(message, key)`**: Encrypts the entire plaintext in segments, producing the complete ciphertext.
- **`all_des_decrypt(message, key)`**: Decrypts the entire ciphertext in segments, recovering the original plaintext.

---

## Installation and Usage

### Requirements
- This is my setup
- **Python 3.11** 
- No additional libraries are required; `base64` is part of the Python standard library.

### Usage Steps

1. Store the plaintext in a `plaintext.txt` file.
2. Run the program and choose between encryption or decryption:
   - Press `1` for encryption: After entering the key, the program outputs the encrypted ciphertext and writes it to `ciphertext.txt`.
   - Press `2` for decryption: After entering the key, the program decrypts the ciphertext and displays the original plaintext.
   - Press `3` to exit.

```bash
# Run the command
python DES_Python.py
```
---

## Usage Examples

### Encryption
1. Save the following text as `plaintext.txt`:
   ```
   IAmABoy!
   ```
2. Run the program and select encryption:
   ```plaintext
   Encrypt press 1   Decrypt press 2   Exit press 3 : 1
   Input the password you want to set: lxhelloo
   ```

   **Output**:

   ![🔐 Encryption Result](encrypt_img.png)
   ```plaintext
   Encrypt press 1   Decrypt press 2   Exit press 3 : 1
   Input the password you want to set: lxhelloo
   Plaintext:  IAmABoy!
   Plaintext 01bits:   0100100101000001011011010100000101000010011011110111100100100001

   Ciphertext 01bits:  1110010001110001011000011111011000011100111111011010000001001001
   Ciphertext:  5HFh9hz9oEk=
   ```
   - Shows the binary representation of the plaintext.
   - Displays the generated ciphertext (Base64 encoded).
   - The ciphertext is saved in `ciphertext.txt`.

### Decryption
1. Run the program and select decryption:
   ```plaintext
   Encrypt press 1   Decrypt press 2   Exit press 3 : 2
   Input your password: lxhelloo
   ```

   **Output**:
   ![Decryption Result](decrypt_img.png)

   ```plaintext
   Encrypt press 1   Decrypt press 2   Exit press 3 : 2
   Ciphertext:  5HFh9hz9oEk=
   Input your password: lxhelloo
   Ciphertext 01bits:   1110010001110001011000011111011000011100111111011010000001001001
   
   Plaintext 01bits:    0100100101000001011011010100000101000010011011110111100100100001
   Plaintext:   IAmABoy!
   ```
   - Shows the binary representation of the decrypted plaintext.
   - Outputs the original plaintext.

---

## Notes
- The key must be 8 characters long, and the program automatically handles the parity bits.
- Plaintext shorter than 64 bits will be padded with zeros.
- Encryption and decryption must use the same key, or the result will be incorrect.
- Ensure the ciphertext file (`ciphertext.txt`) is Base64 encoded for ease of reading and transmission.

---

## 📝 License

This project is licensed under the **MIT License**.  
Please review the terms below to understand your rights and responsibilities:

MIT License

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

**THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.**
