---
description: |
  Recursive content discovery tool. Faster than gobuster with
  automatic recursion into discovered directories.

  Reference values:
    Target URL: http://10.10.10.1
command: |
  # Basic recursive scan
  feroxbuster -u http://10.10.10.1 -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt

  # With extensions and status codes
  feroxbuster -u http://10.10.10.1 -x php,html,txt -s 200,301,302 -o ferox.txt

  # With authentication
  feroxbuster -u http://10.10.10.1 -H "Cookie: session=abc123" -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt
phase:
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
  - https://github.com/epi052/feroxbuster
---
