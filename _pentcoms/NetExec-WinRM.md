---
description: |
  NetExec WinRM module — check access, execute commands,
  and spray credentials over WinRM.

  Reference values:
    Target IP: 10.10.10.1
    Username: pentuser
    Password: P@ssw0rd123
command: |
  # Check WinRM access
  nxc winrm 10.10.10.1 -u pentuser -p 'P@ssw0rd123'

  # Execute command
  nxc winrm 10.10.10.1 -u pentuser -p 'P@ssw0rd123' -x "whoami"

  # PowerShell command
  nxc winrm 10.10.10.1 -u pentuser -p 'P@ssw0rd123' -X "Get-Process"

  # With hash
  nxc winrm 10.10.10.1 -u pentuser -H aad3b435b51404eeaad3b435b51404ee
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
