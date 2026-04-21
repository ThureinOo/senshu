---
description: |
  CPU-based password cracker with auto-detection of hash types.
  Good for quick cracking and format conversion.

  Reference values:
    Hash file: hashes.txt
command: |
  # Auto-detect and crack
  john hashes.txt --wordlist=/usr/share/wordlists/rockyou.txt

  # Crack /etc/shadow
  unshadow /etc/passwd /etc/shadow > unshadowed.txt
  john unshadowed.txt --wordlist=/usr/share/wordlists/rockyou.txt

  # Crack SSH key
  ssh2john id_rsa > ssh_hash.txt
  john ssh_hash.txt --wordlist=/usr/share/wordlists/rockyou.txt

  # Crack zip file
  zip2john archive.zip > zip_hash.txt
  john zip_hash.txt --wordlist=/usr/share/wordlists/rockyou.txt

  # Show cracked passwords
  john --show hashes.txt
phase:
  - Post-Exploitation
target_os:
  - Linux
  - Windows
services: []
items:
  - Hash
techniques: []
network_position:
  - Local
references:
  - https://github.com/openwall/john
---
