---
description: |
  SharpUp — C# port of PowerUp for Windows privilege escalation
  enumeration. Works in constrained language mode environments.
command: |
  # Run all checks
  .\SharpUp.exe audit

  # Specific checks
  .\SharpUp.exe ModifiableServices
  .\SharpUp.exe UnquotedServicePath
  .\SharpUp.exe ModifiableServiceBinaries
  .\SharpUp.exe AlwaysInstallElevated
  .\SharpUp.exe HijackablePaths
phase:
  - PrivEsc
target_os:
  - Windows
services: []
items:
  - Shell
techniques:
  - Token_Impersonation
network_position:
  - Local
references:
  - https://github.com/GhostPack/SharpUp
---
