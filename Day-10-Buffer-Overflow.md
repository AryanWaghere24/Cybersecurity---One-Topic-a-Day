# Day 10 - Buffer Overflow

## What It Is
A Buffer Overflow happens when a program writes more data into a buffer (a fixed size memory block) than it was designed to hold. The extra data spills over into adjacent memory, corrupting it. Attackers exploit this to overwrite critical memory regions — like the return address — and redirect program execution to their own malicious code. It's a memory corruption vulnerability at the lowest level of how programs run.

## How It Works
When a function is called, the program creates a stack frame in memory containing local variables, the saved return address (where to go after the function finishes), and other data. If a local variable is a fixed size buffer and the program copies user input into it without checking the length, an attacker can overflow it.

Simple mental model:
```
Normal stack layout:
[ buffer (100 bytes) ][ saved return address ]

Overflow attack:
[ AAAAAAAAAA...AAAA (200 bytes) ][ overwritten return address → attacker's code ]
```

Steps:
1. Attacker sends input longer than the buffer can hold
2. Extra bytes overwrite the saved return address on the stack
3. When the function returns it jumps to the attacker's address instead
4. Attacker points it to shellcode (malicious machine code) placed in the buffer
5. Shellcode executes — usually spawning a shell

```bash
# Classic test - sending a large pattern to crash the program
python3 -c "print('A' * 500)" | ./vulnerable_program

# If it crashes with a segfault, the program is likely vulnerable to buffer overflow
```
## Real-World Example
The Morris Worm in 1988 was the first self-replicating worm on the internet. One of its three propagation methods was a buffer overflow in the Unix `fingerd` daemon. It exploited the overflow to execute arbitrary code, copy itself to the new machine, and spread further. It infected around 6000 machines — roughly 10% of the entire internet at the time — and caused millions of dollars in damage.

More recently, buffer overflows have been found in consumer routers, industrial control systems, and embedded devices where modern memory protections are often absent or weak.

## Why It Matters
From an attacker's side, a successful buffer overflow gives arbitrary code execution — the holy grail of exploitation. On systems without modern protections it can be straightforward to exploit. Even with protections like ASLR and DEP/NX, advanced techniques like ROP chains can bypass them.

From a defender's side, modern compilers and OS features have made classic buffer overflows harder to exploit — stack canaries detect overwrites, ASLR randomizes memory addresses, and NX/DEP marks the stack non-executable. Using memory-safe languages like Rust or Go eliminates the vulnerability entirely. For C/C++ code, using safe functions like `strncpy` instead of `strcpy` and always validating input length is essential.

## Key Terms
- Buffer Overflow: writing beyond the allocated size of a memory buffer, corrupting adjacent memory
- Stack: a region of memory that stores local variables and return addresses for function calls
- Return Address: the memory address stored on the stack that tells the program where to go after a function finishes
- Shellcode: small machine code payload injected by the attacker that typically spawns a shell
- ASLR (Address Space Layout Randomization): OS feature that randomizes memory addresses each run, making it harder to predict where to jump

## One Tip / Tool

Tool: `pwndbg` + `pwntools` — the standard toolkit for buffer overflow exploitation and CTF challenges

```bash
# install pwntools
pip install pwntools

# basic pwntools script to interact with a vulnerable binary
from pwn import *

p = process('./vulnerable_program')

offset = 112  # number of bytes to reach the return address
ret_address = p64(0xdeadbeef)  # address to jump to

payload = b'A' * offset + ret_address
p.sendline(payload)
p.interactive()
```

For finding the exact offset use `cyclic` from pwntools or `pattern_create` from Metasploit — they generate a unique pattern so you can identify exactly where the return address gets overwritten.

Practice buffer overflows safely on **pwn.college** or **exploit.education** — both are free platforms built specifically for learning binary exploitation.
