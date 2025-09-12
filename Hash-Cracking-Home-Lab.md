# 🧑‍💻 Hash Cracking Home Lab – TryHackMe *Hashing Basics*

This project follows the practice from the **Hashing Basics** room on TryHackMe.  
We explored different types of hashes and learned how to recognize and crack them using **John the Ripper** and **Hashcat**.

---

## 📂 Project Structure

```
Hashing-Basics/
├── Task-6/
│    ├── hash1.txt   # bcrypt ($2a$)
│    ├── hash2.txt   # SHA-256
│    ├── hash3.txt   # SHA-512crypt ($6$)
│    ├── hash4.txt   # MD5
│    └── rockyou.txt # wordlist
```

---

## 🔑 Tools Used
- **John the Ripper** — works in VM, CPU-based.
- **Hashcat** — GPU optimized (but also works on CPU, slower).

---

## 📝 Steps Completed

### 1. bcrypt (hash1.txt)
Example hash:
```
$2a$06$7yoU3Ng8dHTXphAg913cyO6Bjs3K5lBnwq5FJyA6d01pMSrddr1ZG
```

Command (John):
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt --format=bcrypt hash1.txt
john --show hash1.txt
```

✅ Result: password successfully cracked.

---

### 2. SHA-256 (hash2.txt)
Example hash:
```
9eb7ee7f551d2f0ac684981bd1f1e2fa4a37590199636753efe614d4db30e8e1
```

Command (Hashcat):
```bash
hashcat -m 1400 -a 0 hash2.txt /usr/share/wordlists/rockyou.txt
```

✅ Result: password found → `halloween`.

---

### 3. SHA-512crypt (hash3.txt)
Example hash:
```
$6$GQXVvW4EuM$ehD6jWiMsfNorxy5SINsgdlxmAEl3.yif0/c3NqzGLa0P.S7KRDYjycw5bnYkF5ZtB8wQy8KnskuWQS3Yr1wQ0
```

Command (Hashcat):
```bash
hashcat -m 1800 -a 0 hash3.txt /usr/share/wordlists/rockyou.txt
```

⚙️ Status: cracking in progress.

---

### 4. MD5 (hash4.txt)
Example hash:
```
b6b0d451bbf6fed658659a9e7e5598fe
```

Command (Hashcat):
```bash
hashcat -m 0 -a 0 hash4.txt /usr/share/wordlists/rockyou.txt
```

⚡ Expected result: MD5 is very fast, cracked almost instantly.

---

## 📊 Key Takeaways
- Learned to identify hash types: **bcrypt**, **SHA-256**, **SHA-512crypt**, **MD5**.
- Practiced syntax for both `john` and `hashcat`.
- Fixed common mistakes (e.g., `--wordlist` vs `--wordlist=`, correct `-m` codes).
- Produced reproducible examples for portfolio (commands + screenshots).

---

## 🚀 Next Steps
- Add benchmarking (report hash cracking speed in H/s).
- Try different attack modes:
  - `-a 0` (wordlist)  
  - `-a 3` (mask brute-force)  
  - `-a 6/7` (hybrid attacks)  
- Automate workflow with Bash/Python scripts.

---
