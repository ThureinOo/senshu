---
description: |
  Web server vulnerability scanner. Checks for dangerous files,
  outdated software, and misconfigurations.

  Reference values:
    Target IP: 10.10.10.1
command: |
  nikto -h http://10.10.10.1 -o nikto.txt

  # Scan specific port
  nikto -h http://10.10.10.1:8080
phase:
  - Scanning
  - Enumeration
target_os:
  - Linux
  - Windows
services:
  - HTTP
items:
  - No_Creds
techniques: []
network_position:
  - External
  - Internal
references:
  - https://github.com/sullo/nikto
---
