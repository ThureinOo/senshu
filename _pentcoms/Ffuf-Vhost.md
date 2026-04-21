---
description: |
  Fuzz for virtual hosts and subdomains using ffuf.

  Reference values:
    Target IP: 10.10.10.1
    Domain: test.local
command: |
  # Vhost fuzzing
  ffuf -u http://10.10.10.1 -H "Host: FUZZ.test.local" -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -fs 0

  # Directory fuzzing
  ffuf -u http://10.10.10.1/FUZZ -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -mc 200,301,302

  # Extension fuzzing
  ffuf -u http://10.10.10.1/indexFUZZ -w /usr/share/seclists/Discovery/Web-Content/web-extensions.txt -mc 200
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
  - https://github.com/ffuf/ffuf
---
