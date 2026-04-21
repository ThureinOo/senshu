---
description: |
  SSH port forwarding and tunneling techniques for pivoting
  and accessing internal services.

  Reference values:
    Target IP: 10.10.10.1
    Username: john
    Internal Target: 172.16.1.10
command: |
  # Local port forward (access remote service locally)
  ssh -L 8080:172.16.1.10:80 john@10.10.10.1
  # Now access http://127.0.0.1:8080

  # Dynamic SOCKS proxy
  ssh -D 1080 john@10.10.10.1
  # Use with proxychains: socks5 127.0.0.1 1080

  # Remote port forward (expose local service to target)
  ssh -R 4444:127.0.0.1:4444 john@10.10.10.1

  # Double pivot
  ssh -L 8080:172.16.1.10:80 -J john@10.10.10.1 john@172.16.1.10

  # SSH with key
  ssh -i id_rsa -L 8080:127.0.0.1:80 john@10.10.10.1
phase:
  - Post-Exploitation
  - Lateral_Movement
target_os:
  - Linux
services:
  - SSH
items:
  - Username
  - Password
  - Key
techniques:
  - Pivoting_Tunneling
network_position:
  - Internal
references:
  - https://book.hacktricks.wiki/en/generic-methodologies-and-resources/tunneling-and-port-forwarding.html
---
