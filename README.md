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
- rockyou.txt wordlist  
- hash-id.py  
- Kali Linux VM  

---

## Contents
- [MD5 Hash Cracking](#md5-hash-cracking)
- [SHA1 Hash Cracking](#sha1-hash-cracking)
- [Unshadowing `/etc/shadow`](#unshadowing-etcshadow)
- [Cracking Password-Protected ZIP Files](#cracking-password-protected-zip-files)

---

## MD5 Hash Cracking
**Goal:** Demonstrate the process of creating a test MD5 password hash, cracking it with John the Ripper, and verifying the result.

---

### 1: Create a Test Hash File
First, I created a dummy user and assigned them a known MD5 password hash.  
This simulates having extracted a hash from a system for testing purposes.

echo "dummyuser:5f4dcc3b5aa765d61d8327deb882cf99" > hash.txt

### 2: Crack the Hash with John the Ripper
I then fed the hash file into John the Ripper, explicitly defining the format (raw-md5) so John parses and cracks it correctly.
The --wordlist option points to rockyou.txt, a common password dictionary used for penetration testing and training.

john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt

### 3: Display the Cracked Credentials

Finally, I used John’s --show option to neatly display the cracked password in username:password format.
This makes it easier to confirm credentials at a glance.

john --show --format=raw-md5 hash.txt

[images/John Terminal.png](https://github.com/CyberMarcR/images/commit/42b3681d809f507ffaa80f905dfb3ef309009542)

---

## SHA1 Hash Cracking
**Goal:** Demonstrate the process of creating a test SHA1 password hash, cracking it with John the Ripper, and verifying the result.

---

### 1: Create a Test SHA1 Hash

I started by generating a SHA1 hash for a known password (letmein123).
The command used:
echo -n "letmein123" | sha1sum
This returned a SHA1 hash that I could use for testing:
e286977b13f1a89e20d0459207545d15fe1eba08

I then simulated a user by formatting the hash in the style John expects:
dummyuser3:e286977b13f1a89e20d0459207545d15fe1eba08
This line was saved into a file called hash2.txt.

### 2: Crack the Hash with John the Ripper

Using John, I specified the format as raw-sha1 to ensure it interprets the hash correctly.
I also provided the path to the wordlist (rockyou.txt) as usual.
Command:
john --format=raw-sha1 --wordlist=/usr/share/wordlists/rockyou.txt hash2.txt

John successfully cracked the password.

### 3: Reveal the Cracked Credentials

To confirm the result, I used John’s --show flag:
john --show --format=raw-sha1 hash2.txt
Output:
dummyuser3:letmein123
This confirms that the correct password was successfully recovered.
