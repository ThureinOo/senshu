---
description: |
  Brute-force directories and files on a web server using Gobuster.

  Reference values:
    Target URL: http://10.10.10.1
command: |
  gobuster dir -u http://10.10.10.1 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -o gobuster.txt -x php,html,txt
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
  - https://github.com/OJ/gobuster
---
