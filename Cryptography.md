# Cryptography Basics

Cryptography lays the foundation for our digital world. While networking
protocols have made it possible for devices spread across the globe to
communicate, cryptography has made it possible to trust this
communication.

## Importance of Cryptography

Cryptography's ultimate purpose is to ensure secure communication in the
presence of adversaries. The term *secure* includes confidentiality and
integrity of the communicated data. Cryptography can be defined as the
practice and study of techniques for secure communication and data
protection where we expect the presence of adversaries and third
parties. In other words, these adversaries should not be able to
disclose or alter the contents of the messages.

Cryptography is used to protect **confidentiality, integrity, and
authenticity**. In this age, you use cryptography daily, and you're
almost certainly reading this over an encrypted connection. Consider the
following scenarios:

-   **Login Security**: When you log in to TryHackMe, your credentials
    are encrypted and sent to the server so no one can retrieve them by
    snooping on your connection.\
-   **SSH**: When you connect over SSH, your SSH client and the server
    establish an encrypted tunnel so no one can eavesdrop on your
    session.\
-   **Online Banking**: Your browser checks the remote server's
    certificate to confirm you are talking to your bank and not an
    attacker.\
-   **File Integrity**: When you download a file, cryptography provides
    a solution through hash functions to confirm that your file is
    identical to the original one.

Compliance examples:\
- PCI DSS (credit card transactions, requires encryption at rest and in
motion)\
- HIPAA & HITECH (USA healthcare)\
- GDPR (EU), DPA (UK)

These laws and standards show that cryptography is a necessity that
should be present yet usually hidden from direct user access.

------------------------------------------------------------------------

## Plaintext to Ciphertext

-   **Plaintext**: Original, readable message or data before
    encryption.\
-   **Ciphertext**: Scrambled, unreadable version after encryption.\
-   **Cipher**: Algorithm to convert plaintext into ciphertext (and vice
    versa).\
-   **Key**: String of bits the cipher uses to encrypt or decrypt data.\
-   **Encryption**: Process of converting plaintext into ciphertext
    using a cipher and key.\
-   **Decryption**: Reverse process of encryption, converting ciphertext
    back to plaintext using cipher and key.

------------------------------------------------------------------------

## Historical Ciphers

-   **Caesar Cipher**: Shifts letters by a certain number. Insecure by
    today's standards (only 25 possible keys).\
-   **Vigenère Cipher** (16th century)\
-   **Enigma Machine** (WWII)\
-   **One-Time Pad** (Cold War)

------------------------------------------------------------------------

## Types of Encryption

### Symmetric Encryption

-   Same key for encryption and decryption.\
-   Key distribution is the biggest challenge.\
-   Also called *private key cryptography*.\
-   Examples:
    -   **DES**: 56-bit key (broken in \<24 hours by 1999).\
    -   **3DES**: Effective 112-bit security, deprecated in 2019.\
    -   **AES**: Adopted in 2001, key sizes 128/192/256 bits.

### Asymmetric Encryption

-   Uses a **public key** (encryption) and a **private key**
    (decryption).\
-   Also called *public key cryptography*.\
-   Examples: RSA, Diffie-Hellman, ECC.\
-   RSA recommended minimum key size = 2048 bits.\
-   ECC achieves comparable security with shorter keys (e.g., 256-bit
    ECC ≈ 3072-bit RSA).

------------------------------------------------------------------------

## Summary of New Terms

-   **Alice and Bob**: Common fictional characters used in cryptography
    examples.\
-   **Symmetric encryption**: Same key for encryption/decryption, must
    remain secret.\
-   **Asymmetric encryption**: Public key for encryption, private key
    for decryption.

------------------------------------------------------------------------

## Basic Math in Cryptography

### XOR Operation

-   Truth table:

  A   B   A ⊕ B
  --- --- -------
  0   0   0
  0   1   1
  1   0   1
  1   1   0

-   Properties:
    -   A ⊕ A = 0\
    -   A ⊕ 0 = A\
    -   Commutative: A ⊕ B = B ⊕ A\
    -   Associative: (A ⊕ B) ⊕ C = A ⊕ (B ⊕ C)
-   Example:
    -   P = plaintext, K = secret key\
    -   Ciphertext: C = P ⊕ K\
    -   Decryption: C ⊕ K = P

### Modulo Operation

-   Remainder of division: X % Y.\
-   Examples:
    -   25 % 5 = 0\
    -   23 % 6 = 5\
    -   23 % 7 = 2
-   Properties:
    -   Always returns a result in range **0 to n-1**.\
    -   Not reversible (many possible inputs give the same remainder).

------------------------------------------------------------------------
# Public Key Cryptography Basics

## Core Concepts

**Scenario (Analogy with Real Life):**  
Imagine meeting a business partner over coffee to discuss confidential plans:
- **Authentication**: You see/hear the person → you confirm their identity.
- **Authenticity**: You know the words are genuinely from them.
- **Integrity**: The message isn’t altered between speaker and listener.
- **Confidentiality**: You lower your voice so no one else can hear.

**Cyber Realm Comparison:**
- **Authentication**: Confirm you’re talking to the right person.
- **Authenticity**: Verify the message came from the claimed sender.
- **Integrity**: Ensure data isn’t changed during transmission.
- **Confidentiality**: Prevent others from eavesdropping.

### Symmetric vs Asymmetric
- **Symmetric encryption (private key)**: Mainly protects **confidentiality**.
- **Asymmetric encryption (public/private key)**: Adds **authentication, authenticity, and integrity**.

---

## Common Use of Asymmetric Encryption
- Primary use: **Exchanging keys for symmetric encryption**.
- Asymmetric crypto is slower → used just once to establish a **shared symmetric key**, then switch to faster symmetric encryption.

**Analogy:**
- Secret Code → Symmetric key
- Lock → Public key
- Lock’s Key → Private key

---

## RSA (Rivest–Shamir–Adleman)

**Purpose:** Secure data transmission over insecure channels.

**Why it’s secure:**
- Easy to multiply two large primes.
- Extremely hard to factorize a very large number (hundreds of digits).

**Simplified Example:**
- Choose primes: p = 157, q = 199  
- Compute modulus: n = p × q = 31,243  
- Compute φ(n) = (p−1)(q−1) = 30,888  
- Choose e = 163, relatively prime to φ(n)  
- Compute d such that (e × d) mod φ(n) = 1 → d = 379  
- Public key = (n, e) = (31,243, 163)  
- Private key = (n, d) = (31,243, 379)

**Encryption/Decryption:**
- Message: x = 13  
- Encrypt: y = x^e mod n = 13^163 mod 31,243 = 16,341  
- Decrypt: x = y^d mod n = 16,341^379 mod 31,243 = 13

**CTF Context:**
- Common RSA variables:
  - *p, q*: large primes
  - *n*: product of p × q
  - *e*: public exponent
  - *d*: private exponent
  - *m*: plaintext
  - *c*: ciphertext
- Tools: **RsaCtfTool**, **rsatool**

---

## Diffie-Hellman Key Exchange

**Goal:** Establish a **shared secret key** over an insecure channel without prior key exchange.

**Steps:**
1. Public values: choose large prime p and generator g.
2. Alice picks private a, Bob picks private b.
3. Alice computes A = g^a mod p; Bob computes B = g^b mod p.
4. Exchange A and B.
5. Shared secret: Alice computes B^a mod p, Bob computes A^b mod p → both yield g^(ab) mod p.

**Example:**
- p = 29, g = 3  
- Alice: a = 13 → A = 3^13 mod 29 = 19  
- Bob: b = 15 → B = 3^15 mod 29 = 26  
- Shared secret: 19^15 mod 29 = 10, 26^13 mod 29 = 10  ✅

**Note:** Real implementations use very large numbers to ensure security.

**Usage with RSA:**
- DH → Key agreement (shared secret)
- RSA → Authentication, digital signatures, key transport
- Together, they help prevent **MITM attacks**.

---

## SSH and Public Keys

### Authenticating the Server
- SSH warns if the server’s public key isn’t recognized.
- User must verify the fingerprint to prevent **man-in-the-middle** attacks.
- Once accepted, the key is saved in `~/.ssh/known_hosts`.

### Authenticating the Client
- By password (less secure) or by **SSH keys** (preferred).
- Keys are usually **RSA** or **Ed25519**.
- Generate key pair with `ssh-keygen` (e.g. `ssh-keygen -t ed25519`).
- Public key goes to server’s `~/.ssh/authorized_keys`.
- Private key stays with the user and must be kept secret (use chmod 600).
- Optionally protect private keys with a **passphrase** (not sent to server).

### SSH in CTFs
- Placing a key in `authorized_keys` can create a **backdoor**.
- Using SSH gives a more stable shell than a reverse shell (with tab-completion, history, etc.).

---

## Digital Signatures & Certificates

### Digital Signatures
- Provide **authenticity** (who created it) and **integrity** (no tampering).
- Created using **private key**, verified with the **public key**.
- Simplest form: sign a hash of the document with private key; recipient verifies by checking against their own hash of the received document.

### Certificates
- Prove **identity** online (e.g., HTTPS websites).
- Issued and signed by **Certificate Authorities (CAs)**.
- Browsers trust a chain of certificates: site cert → intermediate CA → root CA.
- You can also get free certificates (e.g., **Let’s Encrypt**).
- Modern websites should always use **HTTPS**.

---

## PGP & GPG

- **PGP (Pretty Good Privacy):** Software implementing encryption, signing, and email security.
- **GPG (GnuPG):** Open-source implementation of OpenPGP.

### Key Generation Example
```bash
gpg --full-gen-key
```
- Choose algorithm (RSA, DSA, ECC, etc.)
- Choose key size/curve
- Choose expiry date
- Provide name/email/comment

**Sample Output:**
```
pub   ed25519 2024-08-29 [SC]
      AB7E6AA87B6A8E0D159CA7FFE5E63DBD5F83D5ED
uid   Strategos <strategos@tryhackme.thm>
sub   cv25519 2024-08-29 [E]
```

### Key Handling
- Share **public key** with contacts.
- Keep **private key** secure and optionally protected by a passphrase.
- Backup keys securely.
- To import: `gpg --import backup.key`
- To decrypt: `gpg --decrypt confidential_message.gpg`

---

## Conclusion
- **Cryptography**: Secures communication/data with codes and ciphers.
- **Cryptanalysis**: Study of breaking/bypassing crypto systems.
- **Brute-force attack**: Trying every possible key.
- **Dictionary attack**: Trying words from a dictionary.

---

✅ **Key Takeaways:**
- Public key cryptography = asymmetric keys (public/private).
- Symmetric = fast, good for bulk encryption; asymmetric = secure key exchange & authentication.
- RSA relies on the hardness of factoring large primes.
- Diffie-Hellman enables secure key agreement.
- SSH uses key pairs for secure authentication.
- Digital signatures & certificates ensure authenticity and trust online.
- PGP/GPG are practical tools for secure communication & signing.

# Hashing Basics

## Table of Contents
- [Introduction](#introduction)
- [Hash Functions](#hash-functions)
- [Why Hashing is Important](#why-hashing-is-important)
- [Hash Collisions](#hash-collisions)
- [Insecure Password Storage](#insecure-password-storage)
  - [Storing Passwords in Plaintext](#storing-passwords-in-plaintext)
  - [Using an Insecure Encryption Algorithm](#using-an-insecure-encryption-algorithm)
  - [Using an Insecure Hash Function](#using-an-insecure-hash-function)
- [Using Hashing to Store Passwords](#using-hashing-to-store-passwords)
  - [Rainbow Tables](#rainbow-tables)
  - [Protecting Against Rainbow Tables](#protecting-against-rainbow-tables)
  - [Example of Secure Password Storage](#example-of-secure-password-storage)
  - [Why Not Encryption?](#why-not-encryption)
- [Recognizing Password Hashes](#recognizing-password-hashes)
  - [Linux Passwords](#linux-passwords)
  - [Modern Linux Example](#modern-linux-example)
  - [Windows Passwords](#windows-passwords)
- [Password Cracking](#password-cracking)
  - [Cracking with GPUs](#cracking-with-gpus)
  - [Cracking on VMs](#cracking-on-vms)
- [Integrity Checking](#integrity-checking)
- [HMACs](#hmacs)
- [Hashing vs Encoding vs Encryption](#hashing-vs-encoding-vs-encryption)

---

## Introduction
Imagine you just downloaded a 6 GB file and want to know if it’s identical to the original, bit-for-bit. Or maybe a friend gave you the file on a USB drive—how do you confirm it hasn’t been altered?

👉 The answer is **hashing**: by comparing the **hash values** of the two files. If the hashes are identical, you can be highly confident the files are the same.

A **hash value** is a fixed-size string of characters produced by a **hash function**. A hash function takes an input of any size and produces an output of fixed length.

---

## Hash Functions
- **No keys**: Hashing is not encryption. It’s one-way and not meant to be reversed.
- **Input → Output**: Any size input becomes a fixed-size digest.
- **Avalanche effect**: A tiny change in the input (even 1 bit) results in a very different hash.
- **Fast to compute**, but **computationally infeasible to reverse**.

### Example
The ASCII codes:
- `T` = `54` hex = `01010100` binary
- `U` = `55` hex = `01010101` binary

Only 1 bit is different, yet their MD5/SHA1/SHA256 hashes are completely different.

### Output Format
- Hash functions produce **raw bytes**.
- Common encodings: **hexadecimal** (most common in CLI tools) and **base64**.
- Tools like `md5sum`, `sha1sum`, `sha256sum`, `sha512sum` print hashes in **hex**.

---

## Why Hashing is Important
- Ensures **data integrity** (detects tampering/corruption).
- Provides **password confidentiality**:
  - Servers don’t store plain passwords.
  - Instead, they store the **hash** of your password.
  - During login, the server hashes what you type and compares it with the stored hash.
- Used every day when logging into systems.

---

## Hash Collisions
- A **collision** happens when two different inputs produce the same hash output.
- Because inputs are infinite but outputs are fixed-size, collisions are **unavoidable** (pigeonhole principle).
- Good hash functions make collisions extremely rare.

### Example
- 4-bit hash → only \(2^4 = 16\) possible outputs.
- If you hash 21 different inputs, at least two must collide.

### Broken Hashes
- **MD5** and **SHA-1** are broken (collisions can be engineered). 
- Should not be used for security-critical purposes.

---

## Insecure Password Storage
Bad practices:
1. **Storing passwords in plaintext**
   - Example: RockYou breach (14M plaintext passwords leaked).

2. **Using deprecated encryption**
   - Example: Adobe stored passwords with old encryption and plaintext hints.

3. **Using insecure hash functions without salt**
   - Example: LinkedIn 2012 breach → used unsalted SHA-1.

---

## Using Hashing to Store Passwords
Instead of storing passwords directly:
- Store a **hash of the password**.
- On login, hash the input and compare.

### Rainbow Tables
- Precomputed lookup tables mapping hash → password.
- Effective against unsalted hashes.
- Example snippet:

```
Hash                                Password
02c75fb22c75b23dc963c7eb91a062cc    zxcvbnm
b0baee9d279d34fa1dfd71aadb908c3f    11111
c44a471bd78cc6c2fea32b9fe028d30a    asdfghjkl
```

### Protecting Against Rainbow Tables
- Use a **salt** (random value added to password before hashing).
- Each user gets a **unique salt**.
- Functions like **bcrypt**, **scrypt**, **Argon2**, and **PBKDF2** handle salting automatically.
- Salts don’t need to be secret.

### Example of Secure Password Storage
1. Pick a secure algorithm (e.g., Argon2, bcrypt, scrypt, PBKDF2).  
2. Generate a unique salt (e.g., `Y4UV*^(=go_!`).  
3. Concatenate password + salt.  
   ```
   AL4RMc10kY4UV*^(=go_!
   ```
4. Hash with the chosen algorithm.  
5. Store the **hash** and the **salt**.

### Why Not Encryption?
- Encryption is reversible (needs a key). If the key is stolen, all passwords are exposed.  
- Hashing is one-way, safer for authentication.

---

## Recognizing Password Hashes
When analyzing breaches, you may encounter hashes. Recognizing the algorithm is key.

- **HashID** and similar tools can guess, but aren’t perfect.
- Use context:  
  - Database dumps from web apps → often **MD5** or **SHA-1**.  
  - Windows systems → usually **NTLM (MD4 variant)**.

### Linux Passwords
- Stored in `/etc/shadow` (root-only).  
- Old systems: `/etc/passwd` (insecure, world-readable).
- Format: `$prefix$options$salt$hash`
- Common prefixes:

| Prefix | Algorithm |
|--------|-----------|
| `$y$`  | yescrypt (default in modern Linux)
| `$gy$` | gost-yescrypt (uses GOST R 34.11-2012 + yescrypt)
| `$7$`  | scrypt
| `$2b$, $2y$, $2a$, $2x$` | bcrypt (Blowfish-based)
| `$6$`  | sha512crypt (older Linux)
| `$md5` | SunMD5 (Solaris)
| `$1$`  | md5crypt (FreeBSD)

### Modern Linux Example
```
root@TryHackMe# sudo cat /etc/shadow | grep strategos
strategos:$y$j9T$76UzfgEM5PnymhQ7TlJey1$/OOSg64dhfF.TigVPdzqiFang6uZA4QA1pzzegKdVm4:19965:0:99999:7:::
```
Breakdown of second field:
- `y` → algorithm: **yescrypt**
- `j9T` → parameter
- `76UzfgEM5PnymhQ7TlJey1` → salt
- `/OOSg64dhfF.TigVPdzqiFang6uZA4QA1pzzegKdVm4` → hash

### Windows Passwords
- Stored in the **SAM (Security Accounts Manager)** database.  
- Uses **NTLM** (based on MD4).  
- Hashes look similar to MD4/MD5, so context is crucial.  
- Tools like **mimikatz** can extract them.

---

## Password Cracking
- You **cannot decrypt** a hash. You must **guess inputs, hash them, and compare**.
- Tools: **Hashcat**, **John the Ripper**.

### Cracking with GPUs
- GPUs have thousands of cores, great for hash computations.
- Some algorithms (like bcrypt) are designed to resist GPU speedups.

### Cracking on VMs
- VMs don’t usually have GPU passthrough.  
- CPU cracking works, but slower.  
- Best to run Hashcat directly on host OS with GPU.

---

## Integrity Checking
- Hashing ensures files haven’t changed.  
- Even 1‑bit difference → completely different hash.  
- Example (Fedora ISO `sha256sum` output):

```
SHA256 (Fedora-Workstation-Live-osb-40-1.14.x86_64.iso) = 8d3cb4d99f27eb932064915bc9ad34a7529d5f...
SHA256 (Fedora-Workstation-Live-x86_64-40-1.14.iso)   = dd1faca950d1a8c3d169adf2df4c3644ebb62f...
```

- Also used to **detect duplicate files**.

---

## HMACs
- **HMAC (Hash-based Message Authentication Code)** combines:
  - A **hash function**
  - A **secret key**
- Provides **authenticity** (sender is genuine) and **integrity** (data not modified).

### Steps
1. Pad the secret key to the block size of the hash function.  
2. XOR the key with a constant (ipad).  
3. Hash the result + message.  
4. XOR the key with another constant (opad).  
5. Hash the previous hash + new key.

### Formula
```
HMAC(K, M) = H((K ⊕ opad) || H((K ⊕ ipad) || M))
```

---

## Hashing vs Encoding vs Encryption
- **Hashing**: One-way, fixed-size digest for integrity & authentication.
- **Encoding**: Converts data into another format (e.g., Base64, UTF‑8). Reversible, not for security.
- **Encryption**: Reversible, uses a key, ensures confidentiality.

### Example: Base64 Encoding
```
$ echo "TryHackMe" | base64
VHJ5SGFja01lCg==

$ echo "VHJ5SGFja01lCg==" | base64 -d
TryHackMe
```

---

✨ **Summary:**  
Hashing is a one-way process that produces a fixed-size digest. It’s critical for verifying file integrity and securely storing passwords. Use modern algorithms (bcrypt, scrypt, Argon2, PBKDF2) with unique salts to prevent rainbow table attacks. Remember: **hashing ≠ encryption ≠ encoding**.
