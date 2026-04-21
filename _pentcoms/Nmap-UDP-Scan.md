---
description: |
  Scan for open UDP ports. Important for finding SNMP, DNS, TFTP,
  and other UDP services.

  Reference values:
    Target IP: 10.10.10.1
command: |
  # Top 20 UDP ports
  sudo nmap -sU --top-ports 20 -oN nmap/udp 10.10.10.1

  # Specific UDP ports
  sudo nmap -sU -p 53,67,68,69,111,123,135,137,138,139,161,162,445,500,514,520,631,1434,1900,4500 10.10.10.1
phase:
  - Scanning
target_os:
  - Linux
  - Windows
services:
  - SNMP
  - DNS
items:
  - No_Creds
techniques: []
network_position:
  - External
  - Internal
references:
  - https://nmap.org/book/man.html
---
