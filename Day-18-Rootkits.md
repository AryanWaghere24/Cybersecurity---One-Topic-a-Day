# Day 18 - Rootkits

## What It Is
A Rootkit is a collection of malicious software designed to gain persistent root or admin level access to a system while actively hiding its presence from the operating system, security tools, and the user. The name comes from "root" (the highest privilege on Unix systems) and "kit" (a set of tools). Unlike regular malware that just runs and does damage, a rootkit's primary goal is to stay hidden as long as possible while maintaining access.

## How It Works
Rootkits work by subverting the operating system itself — intercepting system calls, modifying kernel data structures, or hiding at a level below the OS entirely. There are several types based on where they operate:
