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
