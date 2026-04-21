---
description: |
  Manual Windows privilege escalation enumeration commands.
  Check privileges, services, scheduled tasks, and more.
command: |
  # Current user info
  whoami /all
  net user john
  net localgroup Administrators

  # System info
  systeminfo

  # Check privileges (look for SeImpersonate, SeAssignPrimaryToken)
  whoami /priv

  # Unquoted service paths
  wmic service get name,displayname,pathname,startmode | findstr /i "auto" | findstr /i /v "c:\windows"

  # Weak service permissions
  accesschk.exe /accepteula -uwcqv "Authenticated Users" *

  # Scheduled tasks
  schtasks /query /fo LIST /v

  # Running processes
  tasklist /svc

  # Installed software
  wmic product get name,version

  # Network connections
  netstat -ano

  # AlwaysInstallElevated
  reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
  reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated

  # Stored credentials
  cmdkey /list
  dir C:\Users\*\AppData\Roaming\Microsoft\Credentials\*
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
  - https://book.hacktricks.wiki/en/windows-hardening/windows-local-privilege-escalation/index.html
---
