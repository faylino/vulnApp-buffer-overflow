Stack-Based Buffer Overflow Lab (Windows 7)

Overview

This project demonstrates exploitation of a stack-based buffer overflow vulnerability in a vulnerable Windows application running in a controlled lab environment.

The objective was to:

Fuzz the application

Identify EIP control

Calculate exact offset

Identify bad characters

Locate a reliable JMP ESP instruction

Construct final exploit

Achieve reverse shell access

Skills Demonstrated

Stack memory analysis

EIP overwrite techniques

Pattern offset calculation

Little-endian architecture handling

Mona.py module analysis

Shellcode generation with msfvenom

Reverse TCP shell execution

Debugging with Immunity Debugger

Lab Environment

Target: Windows 7 VM

Attacker: Kali Linux VM

Debugger: Immunity Debugger + Mona

Network: Host-only

⚠️ Disclaimer

This exploit was developed in a controlled lab environment for educational purposes only. The vulnerable application was intentionally designed for exploitation training.
