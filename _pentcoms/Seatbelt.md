---
description: |
  Seatbelt — comprehensive Windows host enumeration tool.
  Collects system info, credentials, browser data, and security config.
command: |
  # Run all checks
  .\Seatbelt.exe -group=all

  # Quick system survey
  .\Seatbelt.exe -group=system

  # User-related checks
  .\Seatbelt.exe -group=user

  # Credential hunting
  .\Seatbelt.exe -group=misc

  # Specific checks
  .\Seatbelt.exe CredEnum WindowsVault SavedRDPConnections CloudCredentials
  .\Seatbelt.exe DpapiMasterKeys
  .\Seatbelt.exe InterestingFiles
  .\Seatbelt.exe TokenPrivileges
phase:
  - Post-Exploitation
  - PrivEsc
target_os:
  - Windows
services: []
items:
  - Shell
techniques: []
network_position:
  - Local
references:
  - https://github.com/GhostPack/Seatbelt
---
