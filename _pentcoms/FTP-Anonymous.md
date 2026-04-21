---
description: |
  Check for anonymous FTP access and download files.

  Reference values:
    Target IP: 10.10.10.1
command: |
  # Anonymous login
  ftp 10.10.10.1
  # Username: anonymous
  # Password: (blank or any email)

  # Download all files
  wget -r ftp://anonymous:@10.10.10.1/

  # Nmap FTP scripts
  nmap -sV -p 21 --script="ftp-anon,ftp-bounce,ftp-syst" 10.10.10.1
phase:
  - Enumeration
target_os:
  - Linux
  - Windows
services:
  - FTP
items:
  - No_Creds
techniques: []
network_position:
  - External
  - Internal
references:
  - https://book.hacktricks.wiki/en/network-services-pentesting/pentesting-ftp/index.html
---
