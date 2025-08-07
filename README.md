# John The Ripper Exercises <!-- John the Ripper -->
<img src="https://img.shields.io/badge/-John_the_Ripper-8B0000?style=for-the-badge&logo=linux&logoColor=white"/>

> **Educational use only.** All exercises shown here are performed on virtual machines, lab datasets, or files owned by the author.  
> Do **NOT** attempt password cracking, network scanning, or other offensive techniques on systems you do not own or have explicit permission to test.

---

## Author & Tools
**Author:** MarcusR / [GitHub - CyberMarcR](https://github.com/CyberMarcR)  
**Tools Used:**  
- John the Ripper  
- zip2john  
- rar2john  
- rockyou.txt wordlist  
- hash-id.py  
- Kali Linux VM 

---

## Contents
- [MD5 Hash Cracking](#md5-hash-cracking)
- [SHA1 Hash Cracking](#sha1-hash-cracking)
- [Unshadowing /etc/shadow](#unshadowing-etcshadow)
- [Cracking Password-Protected ZIP Files](#cracking-password-protected-zip-files)
- [Cracking Password-Protected RAR Files](#cracking-password-protected-rar-files)

---

## MD5 Hash Cracking
**Goal:** Demonstrate the process of creating a test MD5 password hash, cracking it with John the Ripper, and verifying the result.

---

### 1: Create a Test Hash File
First, I created a dummy user and assigned them a known MD5 password hash.  
This simulates having extracted a hash from a system for testing purposes.
Command: echo "dummyuser:5f4dcc3b5aa765d61d8327deb882cf99" > hash.txt

### 2: Crack the Hash with John the Ripper
I then fed the hash file into John the Ripper, explicitly defining the format (`raw-md5`) so John parses and cracks it correctly.  
The `--wordlist` option points to `rockyou.txt`, a common password dictionary used for penetration testing and training.
Command: john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt

### 3: Display the Cracked Credentials
Finally, I used John’s `--show` option to neatly display the cracked password in `username:password` format.  
This makes it easier to confirm credentials at a glance.
Command: john --show --format=raw-md5 hash.txt

[images/John Terminal.png](https://github.com/CyberMarcR/images/commit/42b3681d809f507ffaa80f905dfb3ef309009542)

---

