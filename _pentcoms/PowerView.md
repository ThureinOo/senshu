---
description: |
  PowerShell AD enumeration tool. Find users, groups, ACLs,
  trusts, GPOs, and attack paths.
command: |
  # Import
  Import-Module .\PowerView.ps1
  # Or: . .\PowerView.ps1

  # Domain info
  Get-Domain
  Get-DomainController

  # Users
  Get-DomainUser | select samaccountname,description
  Get-DomainUser -SPN  # Kerberoastable

  # Groups
  Get-DomainGroup -Identity "Domain Admins" | select member
  Get-DomainGroupMember -Identity "Domain Admins" -Recurse

  # Computers
  Get-DomainComputer | select dnshostname,operatingsystem

  # Shares
  Find-DomainShare -CheckShareAccess

  # ACLs
  Find-InterestingDomainAcl -ResolveGUIDs

  # GPO
  Get-DomainGPO | select displayname,gpcfilesyspath

  # Trusts
  Get-DomainTrust

  # Find local admin access
  Find-LocalAdminAccess
phase:
  - Enumeration
target_os:
  - Windows
services:
  - LDAP
  - Kerberos
items:
  - Shell
  - Username
  - Password
techniques:
  - BloodHound
  - ACL_Abuse
network_position:
  - Internal
  - Local
references:
  - https://github.com/PowerShellMafia/PowerSploit/blob/master/Recon/PowerView.ps1
---
