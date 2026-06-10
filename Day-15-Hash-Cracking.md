# Day 15 - Hash Cracking

## What It Is
Hash Cracking is the process of recovering the original plaintext password from its hashed value. When applications store passwords they don't save the actual password — they save a hash, a fixed length output produced by running the password through a one-way function like MD5, SHA1, or bcrypt. Hash cracking tries to find the original input that produces the same hash. It's one of the most common post-exploitation steps after dumping a database or system credentials.

## How It Works
A hash function takes any input and produces a fixed length output. The same input always produces the same output, but you can't reverse it mathematically. So instead of reversing it, attackers just try millions of passwords and compare the hashes.

Three main approaches:

- Dictionary attack: try every word in a wordlist, hash each one, compare
- Brute force: try every possible combination of characters systematically
- Rule based attack: take wordlist entries and apply mutations (add numbers, capitalize, substitute characters)

```bash
# identify what type of hash you have first
hash-identifier
# or
hashid 5f4dcc3b5aa765d61d8327deb882cf99

# MD5 example
echo -n "password" | md5sum
# outputs: 5f4dcc3b5aa765d61d8327deb882cf99

# crack with hashcat - dictionary attack
hashcat -m 0 hash.txt /usr/share/wordlists/rockyou.txt

# crack with rules (more powerful)
hashcat -m 0 hash.txt /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule

# common hash types in hashcat
# -m 0    = MD5
# -m 100  = SHA1
# -m 1000 = NTLM (Windows)
# -m 1800 = sha512crypt (Linux /etc/shadow)
# -m 3200 = bcrypt
```
## Real-World Example
In 2012, LinkedIn suffered a massive data breach where 6.5 million password hashes were leaked — all unsalted SHA1. Within days the security community had cracked the majority of them using dictionary attacks and rockyou.txt. Passwords like `linkedin`, `password123`, and `123456` fell instantly. The breach eventually turned out to affect 117 million accounts when the full dataset surfaced years later. The lesson — unsalted weak hashing algorithms are almost as bad as storing plaintext.
