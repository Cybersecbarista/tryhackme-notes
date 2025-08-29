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

