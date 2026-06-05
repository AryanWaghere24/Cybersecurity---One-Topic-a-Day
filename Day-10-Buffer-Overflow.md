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

