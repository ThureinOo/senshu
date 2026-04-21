---
description: |
  DNS enumeration — zone transfers, subdomain discovery,
  and record lookups.

  Reference values:
    Target IP: 10.10.10.1
    Domain: test.local
command: |
  # Zone transfer
  dig axfr test.local @10.10.10.1

  # Enumerate all records
  dig any test.local @10.10.10.1

  # Reverse lookup
  dig -x 10.10.10.1 @10.10.10.1

  # Subdomain brute force
  gobuster dns -d test.local -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -r 10.10.10.1:53

  # dnsenum
  dnsenum --dnsserver 10.10.10.1 test.local

  # Specific record types
  dig test.local MX @10.10.10.1
  dig test.local TXT @10.10.10.1
  dig test.local NS @10.10.10.1
phase:
  - Enumeration
target_os:
  - Linux
  - Windows
services:
  - DNS
items:
  - No_Creds
techniques: []
network_position:
  - External
  - Internal
references:
  - https://linux.die.net/man/1/dig
---
