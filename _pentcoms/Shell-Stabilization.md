---
description: |
  Upgrade a dumb reverse shell to a fully interactive TTY.
  Essential after catching any reverse shell.
command: |
  # Python PTY upgrade
  python3 -c 'import pty;pty.spawn("/bin/bash")'

  # Background the shell
  # Press Ctrl+Z

  # Set terminal options
  stty raw -echo; fg

  # Set environment
  export TERM=xterm
  export SHELL=bash
  stty rows 40 columns 160

  # Alternative: script method
  script /dev/null -c bash
phase:
  - Post-Exploitation
target_os:
  - Linux
services: []
items:
  - Shell
techniques:
  - Reverse_Shell
network_position:
  - Local
references:
  - https://blog.ropnop.com/upgrading-simple-shells-to-fully-interactive-ttys/
---
