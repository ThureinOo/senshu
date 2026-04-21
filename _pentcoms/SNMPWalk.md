---
description: |
  Enumerate SNMP information — system details, running processes,
  installed software, network interfaces, and users.

  Reference values:
    Target IP: 10.10.10.1
command: |
  # SNMPv1/2c with default community string
  snmpwalk -v2c -c public 10.10.10.1

  # System info
  snmpwalk -v2c -c public 10.10.10.1 1.3.6.1.2.1.1

  # Running processes
  snmpwalk -v2c -c public 10.10.10.1 1.3.6.1.2.1.25.4.2.1.2

  # Installed software
  snmpwalk -v2c -c public 10.10.10.1 1.3.6.1.2.1.25.6.3.1.2

  # User accounts
  snmpwalk -v2c -c public 10.10.10.1 1.3.6.1.4.1.77.1.2.25

  # Brute force community strings
  onesixtyone -c /usr/share/seclists/Discovery/SNMP/snmp.txt 10.10.10.1
phase:
  - Enumeration
target_os:
  - Linux
  - Windows
services:
  - SNMP
items:
  - No_Creds
techniques: []
network_position:
  - Internal
references:
  - https://linux.die.net/man/1/snmpwalk
---
