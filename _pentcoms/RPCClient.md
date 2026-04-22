---
description: |
  Enumerate Windows domain info via RPC — users, groups, SIDs,
  password policy.

  Reference values:
    Target IP: 10.10.10.1
    Username: pentuser
    Password: P@ssw0rd123
command: |
  # Null session
  rpcclient -U "" -N 10.10.10.1

  # Authenticated
  rpcclient -U "pentuser%P@ssw0rd123" 10.10.10.1

  # Useful rpcclient commands:
  # enumdomusers        — list domain users
  # enumdomgroups       — list domain groups
  # querydispinfo       — user details
  # queryuser 0x1f4     — query specific user by RID
  # lookupnames admin   — get SID for username
  # getdompwinfo        — password policy
  # querygroupmem 0x200 — members of group by RID
phase:
  - Enumeration
target_os:
  - Windows
services:
  - RPC
  - SMB
items:
  - No_Creds
  - Username
  - Password
techniques: []
network_position:
  - Internal
references:
  - https://www.samba.org/samba/docs/current/man-html/rpcclient.1.html
---
