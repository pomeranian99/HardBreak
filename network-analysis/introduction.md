---
icon: info
---

# Introduction

While analyzing the network communication of an IoT device we may identify services, obtain information or even gain access to the device.

Use tools like `nmap` and `Wireshark` to passively monitor or actively test network and wireless communications (e.g., HTTP, MQTT, CoAP). Sometimes we also encounter proprietary network protocols, which need to be analyzed in depth.&#x20;

We are looking for information like the used operating system, program versions or known vulnerabilities. If we find web applications such as a web server, we should also examine these, as they could allow us to execute code if they are not configured correctly. Learn more about web pentesting on dedicated websites  [Hacktricks](https://book.hacktricks.xyz/pentesting-web/web-vulnerabilities-methodology). If we can login to the device, we may also check configuration settings and access control management.

Goals: Exploit vulnerabilities (RCE, LFI), gain information, firmware extraction\
Things to look for: Protocols (SSH, Telnet, FTP), web
