# Day 15 - Hash Cracking

## What It Is
Hash Cracking is the process of recovering the original plaintext password from its hashed value. When applications store passwords they don't save the actual password — they save a hash, a fixed length output produced by running the password through a one-way function like MD5, SHA1, or bcrypt. Hash cracking tries to find the original input that produces the same hash. It's one of the most common post-exploitation steps after dumping a database or system credentials.
