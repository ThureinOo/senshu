---
description: |
  Enumerate subdomains using various tools and techniques.

  Reference values:
    Domain: test.local
command: |
  # Subfinder (passive)
  subfinder -d test.local -o subdomains.txt

  # Amass (passive + active)
  amass enum -d test.local -o amass.txt

  # Gobuster DNS
  gobuster dns -d test.local -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt

  # Knock
  knockpy test.local

  # crt.sh (certificate transparency)
  curl -s "https://crt.sh/?q=%.test.local&output=json" | jq -r '.[].name_value' | sort -u

  # DNSRecon
  dnsrecon -d test.local -t std
phase:
  - Recon
  - Enumeration
target_os:
  - Linux
  - Windows
services:
  - DNS
  - HTTP
items:
  - No_Creds
techniques: []
network_position:
  - External
references:
  - https://github.com/projectdiscovery/subfinder
---
