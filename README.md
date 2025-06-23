# 🔐 Write-up Task-1: File Encryption and Decryption Using Symmetric AES-256 with PBKDF2

For this assignment, I performed symmetric encryption and decryption on a text file using the **AES-256 algorithm** with secure key derivation (`-pbkdf2`).

---

## 📝 Step 1: Creating the Text File

I opened a terminal and created a text file named `70012.txt` using the command:

```bash
nano 70012.txt
```
Inside this file, I typed my full name, then saved and exited by pressing Ctrl + O, Enter, and Ctrl + X.

![image](https://github.com/user-attachments/assets/0694a70e-595f-4ea7-ad79-01d2708f2c00)

## 🔐 Step 2: Encrypting the File

To encrypt the file using AES-256 with a secure password-based key derivation function, I ran the following command:

```bash
openssl enc -aes-256-cbc -salt -pbkdf2 -in 70012.txt -out encrypted_70012.txt -pass pass:70012
```
+ pbkdf2 ensures a stronger key derivation method.

+ salt adds randomness for added security.

+ pass pass:70012 uses my roll number as the password.

This command created an encrypted file called encrypted_70012.txt.

![image](https://github.com/user-attachments/assets/61d6fe83-f701-43da-9b0f-0e6c5341e3c8)

## 🔓 Step 3: Decrypting the File
To verify the encryption, I decrypted the file back to its original form with:

```bash
openssl enc -aes-256-cbc -d -pbkdf2 -in encrypted_70012.txt -out decrypted_70012.txt -pass pass:70012
```
This produced the file decrypted_70012.txt, containing the original content.

![image](https://github.com/user-attachments/assets/e5c04629-9a38-439e-bb43-02d40a8e8a87)


