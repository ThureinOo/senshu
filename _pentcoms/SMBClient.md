---
description: |
  Connect to SMB shares to list, download, and upload files.

  Reference values:
    Target IP: 10.10.10.1
    Username: john
    Password: password123
command: |
  # List shares (no creds)
  smbclient -L //10.10.10.1 -N

  # List shares (with creds)
  smbclient -L //10.10.10.1 -U john%password123

  # Connect to a share
  smbclient //10.10.10.1/share -U john%password123

  # Download all files recursively
  smbclient //10.10.10.1/share -U john%password123 -c "recurse ON; prompt OFF; mget *"

  # smbmap alternative
  smbmap -H 10.10.10.1 -u john -p password123
phase:
  - Enumeration
target_os:
  - Windows
  - Linux
services:
  - SMB
items:
  - No_Creds
  - Username
  - Password
techniques: []
network_position:
  - Internal
references:
  - https://www.samba.org/samba/docs/current/man-html/smbclient.1.html
---
