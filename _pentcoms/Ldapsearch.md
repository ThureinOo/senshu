---
description: |
  Query LDAP for domain enumeration — users, groups, computers,
  OUs, and more.

  Reference values:
    Target DC: 10.10.10.1
    Domain: test.local
    Username: john
    Password: password123
command: |
  # Anonymous bind — get base DN
  ldapsearch -x -H ldap://10.10.10.1 -s base namingcontexts

  # Authenticated — dump all users
  ldapsearch -x -H ldap://10.10.10.1 -D "john@test.local" -w 'password123' -b "DC=test,DC=local" "(objectClass=user)" sAMAccountName

  # Find domain admins
  ldapsearch -x -H ldap://10.10.10.1 -D "john@test.local" -w 'password123' -b "DC=test,DC=local" "(&(objectClass=group)(cn=Domain Admins))" member

  # Find computers
  ldapsearch -x -H ldap://10.10.10.1 -D "john@test.local" -w 'password123' -b "DC=test,DC=local" "(objectClass=computer)" dNSHostName
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
