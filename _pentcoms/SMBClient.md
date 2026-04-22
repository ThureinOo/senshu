---
description: |
  Connect to SMB shares to list, download, and upload files.

  Reference values:
    Target IP: 10.10.10.1
    Username: pentuser
    Password: P@ssw0rd123
command: |
  # List shares (no creds)
  smbclient -L //10.10.10.1 -N

  # List shares (with creds)
  smbclient -L //10.10.10.1 -U pentuser%P@ssw0rd123

  # Connect to a share
  smbclient //10.10.10.1/share -U pentuser%P@ssw0rd123

  # Download all files recursively
  smbclient //10.10.10.1/share -U pentuser%P@ssw0rd123 -c "recurse ON; prompt OFF; mget *"

  # smbmap alternative
  smbmap -H 10.10.10.1 -u pentuser -p P@ssw0rd123
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
