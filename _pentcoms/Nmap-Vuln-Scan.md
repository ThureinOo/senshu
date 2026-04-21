---
description: |
  Run nmap vulnerability scripts to identify known CVEs and
  misconfigurations on target services.

  Reference values:
    Target IP: 10.10.10.1
command: |
  # Run all vuln scripts
  nmap -sV --script vuln 10.10.10.1

  # Specific service vuln checks
  nmap -p 445 --script smb-vuln* 10.10.10.1
  nmap -p 443 --script ssl-heartbleed 10.10.10.1

  # SMB specific
  nmap -p 445 --script smb-vuln-ms17-010,smb-vuln-ms08-067 10.10.10.1

  # HTTP specific
  nmap -p 80,443 --script http-vuln* 10.10.10.1
phase:
  - Scanning
  - Enumeration
target_os:
  - Linux
  - Windows
services:
  - SMB
  - HTTP
items:
  - No_Creds
techniques: []
network_position:
  - External
  - Internal
references:
  - https://nmap.org/nsedoc/categories/vuln.html
---
