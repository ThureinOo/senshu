---
description: |
  Manual Linux privilege escalation enumeration commands.
  Check SUID, sudo, cron, capabilities, and writable paths.
command: |
  # Current user context
  id && whoami && hostname

  # Sudo permissions
  sudo -l

  # SUID binaries
  find / -perm -4000 -type f 2>/dev/null

  # Capabilities
  getcap -r / 2>/dev/null

  # Writable /etc/passwd
  ls -la /etc/passwd /etc/shadow

  # Cron jobs
  cat /etc/crontab
  ls -la /etc/cron*
  crontab -l

  # Running processes
  ps aux | grep root

  # Network connections
  ss -tlnp

  # Writable paths in PATH
  echo $PATH | tr ':' '\n' | xargs ls -ld 2>/dev/null

  # Kernel version
  uname -a
  cat /etc/os-release

  # Internal services
  ss -tlnp
  cat /etc/hosts
phase:
  - PrivEsc
target_os:
  - Linux
services: []
items:
  - Shell
techniques:
  - Linux_Misconfig
network_position:
  - Local
references:
  - https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html
---
