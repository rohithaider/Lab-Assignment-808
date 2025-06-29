# 🔐 Write-up Task-1 Part-1: File Encryption and Decryption Using Symmetric AES-256 with PBKDF2

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


---
---


# 🔐 Write-up Task-1 Part-2: RSA Key Pair Generation and File Encryption/Decryption Using OpenSSL

In this part of the assignment, I performed asymmetric encryption using RSA public-private key pairs.


## 🔑 Step 1: Generating the Private Key
I created a 2048-bit RSA private key using the command:

```bash
openssl genpkey -algorithm RSA -out private_70012.pem -pkeyopt rsa_keygen_bits:2048
```
![image](https://github.com/user-attachments/assets/4dfb5bca-b688-40cd-8b3e-4a72c77ff5ea)

## 📤 Step 2: Generating the Public Key
After the private key was created, I extracted the corresponding public key by running:

```bash
openssl rsa -pubout -in private_70012.pem -out public_70012.pem
```
![image](https://github.com/user-attachments/assets/bc409bb2-7a3b-4873-a700-1daeb2c62273)

## 🔐 Step 3: Encrypting the File Using the Public Key
With both keys ready, I encrypted 70012.txt using the public key:

```bash
openssl pkeyutl -encrypt -pubin -inkey public_70012.pem -in 70012.txt -out encrypted_rsa_70012.txt
```
I verified that the encrypted file encrypted_rsa_70012.txt was successfully created by listing the files in my directory.

![image](https://github.com/user-attachments/assets/a62103ef-98e7-4183-bd4e-01543a11a729)

## 🔓 Step 4: Decrypting the File Using the Private Key
To ensure the encryption worked, I decrypted the file with the private key:

```bash
openssl pkeyutl -decrypt -inkey private_70012.pem -in encrypted_rsa_70012.txt -out decrypted_rsa_70012.txt
```
After decryption, I confirmed the file decrypted_rsa_70012.txt existed and matched the original content.

![image](https://github.com/user-attachments/assets/fb374c94-3196-4817-8d28-c009e6b32345)

## 🧾 Final Step: Verifying Content
I opened both the encrypted and decrypted files using a text editor (nano) to inspect their contents and ensure everything worked as expected.

![image](https://github.com/user-attachments/assets/5a09524e-a018-4874-a841-5ebdd334a504)

![image](https://github.com/user-attachments/assets/bf69737e-badf-49df-9b5e-fdb9a4432f3f)

---
---
---

# 🔍 Write-up Task-2: Vulnerability Assessment

First, I went to this website ```https://www.tenable.com/downloads/nessus``` and downloaded ```Nessus```.


![image](https://github.com/user-attachments/assets/0fdc41eb-64ef-4ea1-be60-11950e6d2f40)

Then I installed the ```Nessus``` using this command:
```bash
sudo dpkg -i Nessus-*.deb
sudo systemctl start nessusd.service
```

![image](https://github.com/user-attachments/assets/96d0cb85-88ee-4e54-a7e8-8e85a6e9c93a)

After that, I visited https://localhost:8834 to set up Nessus in the browser and created an account, and selected Nessus Essentials.

![image](https://github.com/user-attachments/assets/b48d1fac-d968-4587-8e20-8604453699e7)

![image](https://github.com/user-attachments/assets/d11cd1ab-33eb-4941-b319-85a3a112a8cb)

![image](https://github.com/user-attachments/assets/78ce1e24-59c8-4262-a97e-d8a3b0549585)


After setting up ```Nessus```, I downloaded ```Metasploitable 2``` from the provided link and logged into the VM using the supplied credentials.
For this VM, I created a HOST-ONLY-ADAPTER and assigned the adapter to the VM.

![image](https://github.com/user-attachments/assets/2ed9225e-5e72-4cfa-9525-2958d5657e8b)

Then, I checked the IP address of the Metaspolitable 2 vm using ```ifconfig```

![image](https://github.com/user-attachments/assets/a21cc2f5-816d-4e9f-a2e0-c5650c3a6329)

## Scanning with Nessus

### 🔓 Unauthenticated Scan
* I went to Nessus dashboard → New Scan → Basic Network Scan

* Target = IP of Metasploitable

* Named it "Unauthenticated Scan"

* Ran the scan and exported results as PDF

* Noted the Top 20 vulnerabilities

![image](https://github.com/user-attachments/assets/0f08d480-08fe-4be7-a379-fd049df08ca8)

Here are the top 20 vulnerabilities:

![image](https://github.com/user-attachments/assets/f93b3673-56d4-427a-8216-ce1d93e3f3e0)
![image](https://github.com/user-attachments/assets/543bee7b-ac45-4009-b207-010b914ec99b)

### 🔐 Authenticated Scan

For an authenticated scan, I selected advanced scan and provided the credentials.

![image](https://github.com/user-attachments/assets/677442bf-8851-49d4-b938-7691f488cb89)

![image](https://github.com/user-attachments/assets/6f2e94b8-408c-49f5-a275-1c8a52edffcf)

Here are the top 20 vulnerabilites from authenticated scan:

![image](https://github.com/user-attachments/assets/17a72cc5-9d24-4b9e-8286-c27e0ae4a191)

![image](https://github.com/user-attachments/assets/7c26fe59-d342-45fc-830a-4ae27b8986fa)

## Here are the live links for unauthenticated and authenticated scans:

## 🌐 Live Report Links

- [Unauthenticated Scan](https://fancy-bublanina-b70dad.netlify.app/)
- [Authenticated Scan](https://68591e9e70bccbb184a00292--sparkly-gumdrop-5e2809.netlify.app/)



---
---
---
THANK YOU!







