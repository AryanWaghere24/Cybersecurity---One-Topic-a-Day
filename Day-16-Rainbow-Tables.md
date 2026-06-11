# Day 16 - Rainbow Tables

## What It Is
A Rainbow Table is a precomputed lookup table that maps password hashes back to their original plaintext values. Instead of hashing passwords on the fly during cracking (like hashcat does), rainbow tables do all the computation in advance and store the results. When you want to crack a hash you just look it up in the table — instant result. It's a time-memory tradeoff — you spend storage space to save cracking time.
