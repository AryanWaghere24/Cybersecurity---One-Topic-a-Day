# Day 67 - Symmetric vs Asymmetric Encryption

## What It Is
Encryption is the process of transforming readable data (plaintext) into an unreadable format (ciphertext) using a mathematical algorithm and a key, so that only authorized parties can read it. There are two fundamental approaches: symmetric encryption uses the same key to encrypt and decrypt, while asymmetric encryption uses a mathematically linked key pair — a public key to encrypt and a private key to decrypt. Understanding the difference between these two is foundational to understanding how HTTPS, TLS (day 69), digital certificates (day 68), and virtually every secure communication protocol works.

## How It Works
Both approaches solve the same problem — protecting data from unauthorized access — but in fundamentally different ways with different tradeoffs.

```
Symmetric Encryption:

One key does everything — encrypts AND decrypts
Same key must be shared between sender and receiver
Key exchange is the core challenge — how do you share the key securely?

How it works:
Plaintext + Key → [Encryption Algorithm] → Ciphertext
Ciphertext + Same Key → [Decryption Algorithm] → Plaintext

Common symmetric algorithms:
AES (Advanced Encryption Standard)
- Industry standard, used everywhere
- Key sizes: 128, 192, or 256 bits
- AES-256 is considered quantum-resistant for now
- Used in: file encryption, disk encryption (BitLocker, VeraCrypt),
  VPNs, TLS session encryption

ChaCha20
- Alternative to AES, faster on devices without hardware AES support
- Used in: TLS 1.3, WireGuard VPN, Signal messenger

DES / 3DES (legacy — broken, avoid)
- DES: 56-bit key, cracked in 1997
- 3DES: deprecated, vulnerable to SWEET32 attack

Characteristics:
+ Very fast — can encrypt gigabytes per second
+ Simple — one key to manage
- Key distribution problem — how to securely share the key?
- Doesn't scale — N users need N*(N-1)/2 unique keys

Asymmetric Encryption:

Two mathematically linked keys — public key and private key
Public key: share with everyone, used to encrypt
Private key: keep secret, used to decrypt
What one key encrypts, only the other can decrypt

How it works:
Plaintext + Recipient's Public Key → [Encryption] → Ciphertext
Ciphertext + Recipient's Private Key → [Decryption] → Plaintext

Common asymmetric algorithms:
RSA (Rivest-Shamir-Adleman)
- Most widely used asymmetric algorithm
- Based on difficulty of factoring large prime numbers
- Key sizes: 2048 or 4096 bits recommended
- Used in: TLS handshake, SSH, digital signatures, PGP email

ECC (Elliptic Curve Cryptography)
- Smaller keys, same security level as RSA
- 256-bit ECC ≈ 3072-bit RSA in security strength
- Used in: modern TLS, Bitcoin, Signal, most mobile apps

Diffie-Hellman (DH) / ECDH
- Key exchange algorithm — allows two parties to establish
  a shared secret over an insecure channel without pre-sharing keys
- Foundation of Perfect Forward Secrecy in TLS

Characteristics:
+ Solves key distribution — public key can be shared openly
+ Scales — anyone can encrypt to you using your public key
- Much slower than symmetric — 1000x slower for large data
- Key sizes must be much larger for equivalent security
```

How they work together in practice:
```
Modern secure communication uses BOTH:

1. Asymmetric encryption to securely exchange a symmetric key
   (the TLS handshake — day 69 covers this in detail)
2. Symmetric encryption for the actual data transfer
   (fast AES encryption of all session data)

This hybrid approach gets the best of both:
- Security of asymmetric (no pre-shared key needed)
- Speed of symmetric (fast bulk data encryption)

Real example — HTTPS:
1. Browser gets server's public key (from TLS certificate)
2. Browser generates a random session key
3. Browser encrypts session key with server's public key → sends it
4. Server decrypts with its private key → both have the session key
5. All further communication encrypted with fast AES using session key
```

## Real-World Example
The 2013 Snowden revelations revealed that the NSA had been working to undermine cryptographic standards — specifically targeting the random number generator in an elliptic curve algorithm (Dual_EC_DRBG) which was suspected of containing a backdoor allowing the NSA to predict "random" numbers and break encryption. This led to widespread distrust of closed cryptographic standards and accelerated the industry shift toward open, peer-reviewed algorithms like those recommended by the IETF. It also demonstrated that the choice of cryptographic algorithm matters enormously — weak or backdoored algorithms make strong key management irrelevant.

## Why It Matters
From an attacker's side, cryptography attacks target the weakest link — not usually the algorithm itself (breaking AES-256 directly is computationally infeasible) but the implementation: weak random number generators, short keys, deprecated algorithms (MD5, DES, RC4), key mismanagement, or side-channel attacks that extract keys through timing measurements or power analysis.

From a defender's side, choosing modern cryptographic algorithms and correct key sizes is the foundation of any security architecture. Using deprecated algorithms like MD5 for password hashing (day 15), DES for data encryption, or RSA-1024 for key exchange creates exploitable weaknesses. Cryptographic agility — designing systems to swap algorithms when needed — is increasingly important as quantum computing threatens current asymmetric algorithms.
