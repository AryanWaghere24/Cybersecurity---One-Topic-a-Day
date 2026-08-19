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
