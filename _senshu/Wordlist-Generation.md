---
description: |
  Wordlist generation techniques — CeWL website scraping, username generation from names, Crunch patterns, Hashcat rule-based expansion, and common wordlist locations.
command: |
  # CeWL — generate wordlist from website
  cewl http://10.10.10.27 -d 3 -m 5 -w wordlist.txt
  cewl http://10.10.10.27 --with-numbers -w wordlist.txt

  # Username generation from names
  # Format: first.last, f.last, firstl, flast
  # Use username-anarchy or manually:
  cat names.txt | while read name; do
    first=$(echo $name | cut -d' ' -f1 | tr '[:upper:]' '[:lower:]')
    last=$(echo $name | cut -d' ' -f2 | tr '[:upper:]' '[:lower:]')
    echo "$first.$last"
    echo "${first:0:1}.$last"
    echo "$first${last:0:1}"
    echo "${first:0:1}$last"
  done > users.txt

  # Crunch — generate custom patterns
  crunch 8 8 -t P@ss%%^^ -o passwords.txt
  crunch 6 6 0123456789 -o pins.txt

  # Hashcat rule-based (from existing words)
  hashcat raw.txt --stdout -r /usr/share/hashcat/rules/best64.rule > passwords.txt

  # Reverse strings (check reversed passwords)
  cat passwords.txt | rev >> passwords.txt

  # Common wordlist locations
  /usr/share/wordlists/rockyou.txt
  /usr/share/wordlists/dirb/big.txt
  /usr/share/wordlists/dirb/common.txt
  /usr/local/share/seclists/Discovery/Web-Content/big.txt
  /usr/local/share/seclists/Usernames/xato-net-10-million-usernames.txt
items:
  - No_Creds
phase:
  - Reconnaissance
target_os:
  - Linux
  - Windows
services: []
techniques: []
references:
  - https://github.com/digininja/CeWL
  - https://github.com/urbanadventurer/username-anarchy
  - https://hashcat.net/wiki/doku.php?id=rule_based_attack
---
