---
description: |
  Enumerate valid usernames via SMTP VRFY/EXPN/RCPT commands.

  Reference values:
    Target IP: 10.10.10.1
command: |
  # smtp-user-enum
  smtp-user-enum -M VRFY -U /usr/share/seclists/Usernames/Names/names.txt -t 10.10.10.1

  # Manual enumeration via telnet
  telnet 10.10.10.1 25
  VRFY john
  EXPN admin

  # Nmap scripts
  nmap -p 25 --script smtp-enum-users,smtp-commands,smtp-vuln-cve2010-4344 10.10.10.1

  # Send email (for phishing in OSEP)
  swaks --to victim@test.local --from attacker@test.local --server 10.10.10.1 --body "Click here" --header "Subject: Important"
phase:
  - Enumeration
target_os:
  - Linux
  - Windows
services:
  - SMTP
items:
  - No_Creds
techniques: []
network_position:
  - External
  - Internal
references:
  - https://github.com/pentestmonkey/smtp-user-enum
---
