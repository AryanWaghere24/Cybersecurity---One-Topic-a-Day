# Day 15 - Hash Cracking

## What It Is
Hash Cracking is the process of recovering the original plaintext password from its hashed value. When applications store passwords they don't save the actual password — they save a hash, a fixed length output produced by running the password through a one-way function like MD5, SHA1, or bcrypt. Hash cracking tries to find the original input that produces the same hash. It's one of the most common post-exploitation steps after dumping a database or system credentials.

## How It Works
A hash function takes any input and produces a fixed length output. The same input always produces the same output, but you can't reverse it mathematically. So instead of reversing it, attackers just try millions of passwords and compare the hashes.

Three main approaches:

- Dictionary attack: try every word in a wordlist, hash each one, compare
- Brute force: try every possible combination of characters systematically
- Rule based attack: take wordlist entries and apply mutations (add numbers, capitalize, substitute characters)
