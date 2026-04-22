---
description: |
  Query LDAP for domain enumeration — users, groups, computers,
  OUs, and more.

  Reference values:
    Target DC: 10.10.10.1
    Domain: test.local
    Username: pentuser
    Password: P@ssw0rd123
command: |
  # Anonymous bind — get base DN
  ldapsearch -x -H ldap://10.10.10.1 -s base namingcontexts

  # Authenticated — dump all users
  ldapsearch -x -H ldap://10.10.10.1 -D "pentuser@test.local" -w 'P@ssw0rd123' -b "DC=test,DC=local" "(objectClass=user)" sAMAccountName

  # Find domain admins
  ldapsearch -x -H ldap://10.10.10.1 -D "pentuser@test.local" -w 'P@ssw0rd123' -b "DC=test,DC=local" "(&(objectClass=group)(cn=Domain Admins))" member

  # Find computers
  ldapsearch -x -H ldap://10.10.10.1 -D "pentuser@test.local" -w 'P@ssw0rd123' -b "DC=test,DC=local" "(objectClass=computer)" dNSHostName
phase:
  - Enumeration
target_os:
  - Windows
services:
  - LDAP
items:
  - No_Creds
  - Username
  - Password
techniques: []
network_position:
  - Internal
references:
  - https://linux.die.net/man/1/ldapsearch
---
