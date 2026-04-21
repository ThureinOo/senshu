---
description: |
  WordPress vulnerability scanner. Enumerates plugins, themes,
  users, and known vulnerabilities.

  Reference values:
    Target URL: http://10.10.10.1
command: |
  # Basic scan
  wpscan --url http://10.10.10.1 --enumerate vp,vt,u

  # With API token for vulnerability data
  wpscan --url http://10.10.10.1 --enumerate vp,vt,u --api-token YOUR_TOKEN

  # Brute force login
  wpscan --url http://10.10.10.1 -U admin -P /usr/share/wordlists/rockyou.txt
phase:
  - Enumeration
  - Exploitation
target_os:
  - Linux
  - Windows
services:
  - HTTP
items:
  - No_Creds
  - Username
techniques:
  - Web_Injection
network_position:
  - External
  - Internal
references:
  - https://github.com/wpscanteam/wpscan
---
