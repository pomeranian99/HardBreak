---
icon: info
---

# Introduction

One of the most promising attack vectors is the hardware of an IoT device. Attackers have numerous methods to extract sensitive information, such as using logic analyzers to sniff communication lines or attempting to escalate their privileges.

A very common target is to extract the firmware of a device, which stores all code and therefore also all secrets. Once we opened the device, we should look out for debug interfaces like UART, JTAG or SWD, which allows us to communicate directly to the device. These interfaces are often not secured and are a very promising way to dump the firmware from devices. We could also attempt to dump the firmware from a flash chip over SPI. &#x20;

Once the firmware is extracted, tools like `binwalk`, `Ghidra`, or `radare2` can be used to reverse-engineer and analyze the firmware, looking for hardcoded credentials, encryption keys, and exploitable vulnerabilities.

Things to look for: Memory chips, debug interfaces, communication lines

Goal: Extract firmware, sniff sensitive data from communication interfaces
