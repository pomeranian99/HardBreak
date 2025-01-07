---
icon: browser
---

# Firmware Extraction Methods

## Firmware Extraction Methods

Firmware is the software embedded in a device's hardware, often critical for its operation. Extracting and analyzing it is crucial to understqnd the device's functionality and structure and establish a foothold by analysing, through methods of reverse engineering, or modifying the firmware and reflashing a device.

But before you fire up [Binwalk](https://github.com/ReFirmLabs/binwalk) or [Ghidra](https://github.com/NationalSecurityAgency/ghidra) and start analyzing, reversing and establishing your foothold, you first need to obtain the firmware itself.

Obtaining the firmware from devices can be done in several different ways. Depending on the target device, firmware can be extracted through physical, semi-physical, or software-only methods. This page covers both invasive and non-invasive approaches.

### Non-Invasive Methods

These methods do not involve opening or physically tampering with the device and are often less risky.

#### Downloading from the Manufacturer Website

Manufacturers often host firmware files on their official websites for manual updates.

**Tools**

For this method there are no specific tools required, however you can benefit from a proficiency in techniques such as `google dorking` and others detailed within the Reconaissance chapter

**Steps of retrieving the software from the Manufacturer Website**

1. Search the vendor’s website or forums for downloadable firmware.
2. Simply download or use tools like wget to scrape and download files if necessary.
3. Verify the downloaded file’s integrity and match its expected format.

{% hint style="warning" %}
These firmware could be malicious or in unexpected formats. Be wary when downloading firmware from sources you do not trust 100%, always take precautionary measures when retrieving binaries or files in general from forums or website.
{% endhint %}

#### MitM Attack on the Update Process

Many devices update their firmware via OTA updates. Capturing these updates can provide the firmware file.

Although many devices use HTTPS, complicating the process of intercepting, it is still possible if you are able to intercept the certificates

**Tools required**

* Packet capture tools (e.g., Wireshark) to monitor and intercept update traffic.
* Proxies (e.g., mitmproxy, [mitmrouter](https://github.com/nmatt0/mitmrouter)) to redirect and inspect update requests and device network traffic.

**Steps of a MitM attack on the OTA update process**

1. Set up a network sniffer or proxy.
2. Place the device on the same network and trigger an OTA update.
3. Capture the firmware file during download.

TODO: add practical example

#### Dumping Firmware through a Vulnerability

Exploiting a vulnerability in the device’s software or configuration to access and dump firmware.

**Tools**

* Vulnerability scanning tools (e.g., Nessus, Nmap).
* Custom scripts or exploit frameworks.

**Steps**

1. Identify vulnerabilities in the device’s firmware or communication.
2. Use appropriate tools or scripts to exploit the vulnerability and gain a foothold on the device and/or retrieve the firmware.

TODO: add practical example

### Semi-Invasive Methods

These approaches require minimal physical interaction with the device but stop short of full disassembly.

#### Exposed interfaces

**Tools**

Depending on the interface that is exposed, various different tools might be required:

* USB-to-UART adapters.
* Debugging software (e.g., OpenOCD for JTAG).

**Step to extracting the firmware through an exposed interface**

1. Locate debug interfaces on the device’s casing or accessible panels.
2. Use appropriate tools and protocol to interact with the interface and extract the firmware as detailed within the various pages below:

* [UART](/hardware-hacking/interface-interaction/uart/extract-firmware-using-uart.md)
* [SPI](/hardware-hacking/interface-interaction/spi/extract-firmware-using-spi.md)
* [JTAG/SWD](/hardware-hacking/interface-interaction/jtag-swd/extract-firmware-using-jtag-swd.md)
* [I2C](/hardware-hacking/interface-interaction/i2c.md)

### Invasive Methods

These methods involve opening the device and physically interacting with the components on the board. These usually involve desoldering the component, rendering it unusable, unless perfectly reassebled.

Use these invasive methods only when non-invasive methods fail, and you have permission to "break" the device.

{% hint style="info" %}
There is a fine line between the semi-invasive methods and the invasive methods, especially for the non-BGA packages. It might be possible to open up the device and read out the contents of a chip without desoldering anyting, but using something like a clip adapter. This adapter makes it possible to just apply it over the chip and already interact with the flash chip on the device without the need for desoldering.
{% endhint %}

{% hint style="warning" %}
Do keep in mind that interacting in the way as described above, may power the chip when doing the actual reading, leading to possible loss of data, malfunction or unwanted behaviour.
{% endhint %}

#### Introduction to Chip Packages:

Knowing what chip you have on the device is essential to knowing which reader and extraction method you may or may not need to use when you are attempting to perform a chip-off extraction. A few of the most common package types are listed below

ToDo: add a note/guide on how to identify the chip type (datasheet, marking, visual)

{% tabs %}
{% tab title="TSOP Package" %}
```
TSOP (Thin Small Outline Package): A type of rectangular IC package where pins extend outward on both sides. It is commonly used for flash memory chips.

ToDo: add images and examples of different package sizes of TSOP packages
```
{% endtab %}

{% tab title="QFP Package" %}
```
QFP (Quad Flat Package): A flat, square IC package with pins extending on all four sides, ideal for high-density chip designs.  

ToDo: add images and examples of different package sizes of QFP packages
```
{% endtab %}

{% tab title="BGA Package" %}
```
BGA (Ball Grid Array): A package type with connections in the form of solder balls on the underside of the chip, allowing for higher pin density but requiring specialized tools for handling.

ToDo: add images and examples of different package sizes of BGA Packages
```
{% endtab %}

{% tab title="UFS BGA Package" %}
```
UFS (Universal File Storage) chips use the BGA packaging style but are specifically designed for high-speed data storage applications like smartphones and automotive systems. They are complex to read out and require specialized readers to decode the more advanced protocols

ToDo: add images and examples of different package sizes of BGA Packages
```
{% endtab %}
{% endtabs %}

#### Chip-Off Extraction of a QFP, TSOP, and Other Non-BGA Packages

Non-BGA packages are generally easier to desolder and interface with. They are less technically demanding and require minimal specialized equipment

**Tools:**

* Chip readers and programmers (e.g. Xgecu T56).
* Hot air stations or chip removal tools.

**Steps to perform a chip-off extraction of a non-BGA package**

1. Desolder the chip using a hot air station or similar tool.
2. Place the chip in a compatible reader and dump the contents.

{% hint style="warning" %}
* Ensure proper orientation and connection during the reading process. (possibly label the orientation)
* Avoid overheating the chip to prevent data loss.
{% endhint %}

#### Chip-Off Extraction of a BGA-Package Flash Chip

Performing a chip-off extraction with BGA-packaged flash chips require more advanced tools and expertise.

**Tools**

* Rework station with precise temperature control for BGA chip removal.
* Soldering Flux
* BGA chip readers and adapters.
* Optional & Advanced: Infrared rework stations for precise temperature control.

**Steps to perform a chip-off extraction of a BGA package**

* Precaution: Preheat the board to reduce thermal stress.
* Apply soldering flux to the area of the chip
* Remove the BGA chip carefully using a rework station (with precise temperature control).
* Use a specialized adapter to connect the chip to a reader and extract the data.

#### Chip-Off Extraction of UFS Flash in BGA Package

{% hint style="info" %}
UFS Flash Chips are a newer counterpart to the eMMC chips that we usually see. as of this moment they are quite rare and require a dedicated programmer to read these out (e.g. [UFI-UFS Prog Tool Suite](https://www.ufi-box.com/pages/ufi-ufs-prog))
{% endhint %}

ToDo: Add logical next blocks
