---
icon: magnifying-glass
---

# OSINT (search the web)

OSINT (Open Source Intelligence) is the practice of collecting information from publicly available resources. In the context of IoT (Internet of Things) devices, this refers to gathering intelligence from a variety of sources to understand the ecosystem, identify potential vulnerabilities, or profile devices connected to networks. OSINT for a device is often overlooked. What to look for:

### **1. Documentation**

* Manufacturers release documentation detailing device functionalities.
* Key actions include Backup, USB Port usage, and Firmware Updates.

<figure><img src="../../../.gitbook/assets/image (78).png" alt=""><figcaption><p>Search for user manuals or documentation of your target</p></figcaption></figure>

### **2. Firmware Updates**

* Public firmware may be available on manufacturers' websites.
* Allows for reverse engineering without dumping firmware directly from the device.

<figure><img src="../../../.gitbook/assets/image (77).png" alt=""><figcaption><p>Example: Netgear offers free firmware downloads</p></figcaption></figure>

### **3. Default Credentials**

* Devices often come with default credentials that are easily exploitable, check websites for them
* A great database of default passwords can be found on [Github](https://github.com/ihebski/DefaultCreds-cheat-sheet/blob/main/DefaultCreds-Cheat-Sheet.csv)

### **4. Lookout for CVEs and blogs**

* Community forums may reveal unreported vulnerabilities.
* Security research papers can highlight known exploits and weaknesses.
* Search on [CVEdetails](https://www.cvedetails.com/) for your target or vendor

### 5. FCC ID

* If your device can transmit data over radio frequencies and is sold in the USA, it requires an FCC ID
* Often you can find it somewhere on the device label:

<figure><img src="../../../.gitbook/assets/image (79).png" alt="" width="383"><figcaption><p>FCC ID found</p></figcaption></figure>

* On [https://fccid.io/](https://fccid.io/) you can search the FCC ID and will get documentation, external photos and very interesting for us: Internal photos

<figure><img src="../../../.gitbook/assets/image (80).png" alt="" width="563"><figcaption><p>Internal Photos of target device</p></figcaption></figure>

* Here an example, where we can already spot a potential debug interface:

<figure><img src="../../../.gitbook/assets/image (81).png" alt="" width="563"><figcaption><p>Potential UART found on FCC picture</p></figcaption></figure>
