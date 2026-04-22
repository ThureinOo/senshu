---
description: |
  Find accounts with Kerberos delegation configured —
  unconstrained, constrained, and RBCD.

  Reference values:
    Target DC: 10.10.10.1
    Domain: test.local
    Username: pentuser
    Password: P@ssw0rd123
command: |
  impacket-findDelegation test.local/pentuser:P@ssw0rd123 -dc-ip 10.10.10.1
phase:
  - Enumeration
target_os:
  - Windows
services:
  - LDAP
  - Kerberos
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
