---
description: |
  GPU-accelerated password cracking. Common hash modes for pentest exams.

  Reference values:
    Hash file: hashes.txt
    Wordlist: /usr/share/wordlists/rockyou.txt
command: |
  # NTLM
  hashcat -m 1000 hashes.txt /usr/share/wordlists/rockyou.txt

  # NTLMv2 (Responder captures)
  hashcat -m 5600 hashes.txt /usr/share/wordlists/rockyou.txt

  # Kerberoast (TGS-REP)
  hashcat -m 13100 hashes.txt /usr/share/wordlists/rockyou.txt

  # AS-REP Roast
  hashcat -m 18200 hashes.txt /usr/share/wordlists/rockyou.txt

  # MD5
  hashcat -m 0 hashes.txt /usr/share/wordlists/rockyou.txt

  # SHA256
  hashcat -m 1400 hashes.txt /usr/share/wordlists/rockyou.txt

  # With rules
  hashcat -m 1000 hashes.txt /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule
phase:
  - Post-Exploitation
target_os:
  - Linux
  - Windows
services: []
items:
  - Hash
techniques:
  - Kerberoasting
  - AS-REP_Roasting
  - NTLM_Relay_Poisoning
network_position:
  - Local
references:
  - https://hashcat.net/hashcat/
---
