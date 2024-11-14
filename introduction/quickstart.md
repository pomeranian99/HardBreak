---
icon: circle-chevron-right
---

# Methodology

IoT devices have a lot of functionalities. Let's take the example of an alarm system: It probably has a key fob, a mobile app, radio frequency communication, maybe a webserver, which can be accessed over Wi-Fi etc. Therefore, we need a good strategy on how to tackle a security assessment of those complex devices.

### 1. **Initial Recon and Information Gathering**

Hardware hacking often starts without the hardware. Even before we receive the device we want to test, we can already start gathering information about the device:  such as datasheets, manuals, and online resources. If we receive the device, we should look at it from the outside and identify any exposed ports or interfaces such as UART, JTAG, USB, Ethernet, or wireless interfaces like Wi-Fi and Bluetooth. If the device has an FCC ID there is will be most likely a complete tear down available here: [https://fcc.io/](https://fcc.io/). It's useful for getting a view inside without the need to open the device. Sometimes also a firmware update can be downloaded from the manufacturer's website, which we can analyze. Also look out for public CVEs, blog entries or research, which has been performed on your device.

### 2. Network Analysis

Use tools like `nmap` and `Wireshark` to passively monitor or actively test network and wireless communications (e.g., HTTP, MQTT, CoAP). We are looking for information like the used operating system, program versions or known vulnerabilities. If we find web applications such as a web server, we should also examine these, as they could allow us to execute remodeled code if they are not configured correctly. Learn more about Web-Pentesting on  [Hacktricks](https://book.hacktricks.xyz/pentesting-web/web-vulnerabilities-methodology). If we can login to the device, we may also check configuration settings and access control management.

### 3. **Hardware Analysis (closed device)**

Before opening a device, we should first check out external facing interfaces like RF communication, Bluetooth or USB ports.  Tools like `USBPcap` can passively monitor USB communication. If the host system is Windows based kiosk-escapes may be possible or the use of the [rubber ducky](https://shop.hak5.org/products/usb-rubber-ducky). Also, the device may have a display and buttons or even a keyboard: check out if you can do anything, which was not intended.

Software-defined radios (SDRs) like HackRF or RTL-SDR can be used to capture and analyze RF traffic. Here you might have to practice your reverse engineering skills to be able to understand the communication.

### 4. **Hardware Analysis (opened device)**

{% hint style="warning" %}
Watch out for tamper protection, as this might make the device unusable once its triggered. Also be careful when working on an opened device: You don't want to break the device or hurt yourself.
{% endhint %}

Probably the most promising attack vector is the hardware of a IoT device. There are countless methods, where attackers try to extract sensitive information, e.g. by sniffing communication lines using logic analyzers, or attempt to escalate their privileges.&#x20;

A very common target is to extract the firmware of a device, which stores all code and therefore also all secrets. Once we opened the device, we should look out for debug interfaces like UART, JTAG or SWD, which allows us to communicate directly to the device. These interfaces are often not secured and are a very promising way to dump the firmware from devices. We could also attempt to dump the firmware from a flash chip over SPI. &#x20;

Once the firmware is extracted, tools like `binwalk`, `Ghidra`, or `radare2` can be used to reverse-engineer and analyze the firmware, looking for hardcoded credentials, encryption keys, and exploitable vulnerabilities.

### 5. **Advanced Exploitation**

Hardware attacks, such as power analysis or fault injection, can be attempted to bypass security measures, such as read-out protections. These methods are invasive and should be carried out carefully, as they carry a risk of breaking the device. Another attack vector is to modify the firmware by changing the root password for example and rewrite it to the device.

### 6. **Components Analysis**

We should also investigate components an IoT device may have. For an alarm system this could be something like the key fob or a mobile app. Vulnerabilities in these components could give us access to the main control station and shouldn't be overlooked.
