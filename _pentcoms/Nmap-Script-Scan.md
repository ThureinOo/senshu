---
description: |
  Run targeted nmap NSE scripts for specific service enumeration.

  Reference values:
    Target IP: 10.10.10.1
command: |
  # SMB enumeration
  nmap -p 445 --script smb-enum-shares,smb-enum-users,smb-os-discovery 10.10.10.1

  # LDAP enumeration
  nmap -p 389 --script ldap-search,ldap-rootdse 10.10.10.1

  # HTTP enumeration
  nmap -p 80,443 --script http-title,http-headers,http-methods,http-enum 10.10.10.1

  # DNS enumeration
  nmap -p 53 --script dns-brute,dns-zone-transfer --script-args dns-brute.domain=test.local 10.10.10.1

  # RPC/MSRPC
  nmap -p 135 --script msrpc-enum 10.10.10.1
phase:
  - Enumeration
target_os:
  - Linux
  - Windows
services:
  - SMB
  - LDAP
  - HTTP
  - DNS
  - RPC
items:
  - No_Creds
techniques: []
network_position:
  - External
  - Internal
references:
  - https://nmap.org/nsedoc/
---
