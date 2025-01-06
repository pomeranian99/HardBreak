# Firmware Extraction Methods
Firmware is the software embedded in a device's hardware, often critical for its operation. Extracting and analyzing it is crucial to gain an insight into the device and establish a foothold by analysing, through methods of reverse engineering, or modifying the firmware and reflashing a device.

But before you can start analyzing, reversing and establishing your foothold, you first need to obtain the firmware itself.

Obtaining the firmware from devices can be done in several different ways.  Depending on the target device, firmware can be extracted through physical, semi-physical, or software-only methods. This page covers both invasive and non-invasive approaches.

## Non-Invasive Methods

These methods do not involve opening or physically tampering with the device and are often less risky.

### Downloading from the Manufacturer Website
Manufacturers often host firmware files on their official websites for manual updates.

#### Tools
For this method there are no specific tools required, however you can benefit from a healthy knowledge on `google dorking` and other techniques detailed within the [Reconaissance](./reconnaissance/README.md) chapter

#### Steps of retrieving the software from the Manufacturer Website 
1. Search the vendor’s website or forums for downloadable firmware.
2. Simply download or use tools like wget to scrape and download files if necessary.
3. Verify the downloaded file’s integrity and match its expected format.

{% hint style="warning" %}
Be wary when downloading firmware from sources you do not trust 100%, always take precautionary measures when retrieving binaries or files in general from forums or website
{% endhint %}


### MitM Attack on the Update Process
Many devices update their firmware via OTA updates. Capturing these updates can provide the firmware file.

#### Tools required
- Packet capture tools (e.g., Wireshark) to monitor and intercept update traffic.
- Proxies (e.g., mitmproxy, [mitmrouter](https://github.com/nmatt0/mitmrouter)) to redirect and inspect update requests and device network traffic.

#### Steps of a MitM attack on the OTA update process

1. Set up a network sniffer or proxy.
2. Place the device on the same network and trigger an OTA update.
3. Capture the firmware file during download.


TODO: add practical example


### Dumping Firmware through a Vulnerability
Exploiting a vulnerability in the device’s software or configuration to access and dump firmware.

#### Tools
- Vulnerability scanning tools (e.g., Nessus, Nmap).
- Custom scripts or exploit frameworks.

#### Steps
1. Identify vulnerabilities in the device’s firmware or communication.
2. Use appropriate tools or scripts to exploit the vulnerability and gain a foothold on the device and/or retrieve the firmware.


TODO: add practical example

## Semi-Invasive Methods
These approaches require minimal physical interaction with the device but stop short of full disassembly.


### Exposed interfaces 

#### Tools
Depending on the interface that is exposed, various different tools might be required:
- USB-to-UART adapters.
- Debugging software (e.g., OpenOCD for JTAG).

#### Step to extracting the firmware through an exposed interface
1. Locate debug interfaces on the device’s casing or accessible panels.
2. Use appropriate tools and protocol to interact with the interface and extract the firmware as detailed within the various pages below:

- [UART](./interface-interaction/uart/extract-firmware-using-uart.md)
- [SPI](./interface-interaction/spi/extract-firmware-using-spi.md)
- [JTAG/SWD](./interface-interaction/jtag-swd/extract-firmware-using-jtag-swd.md)
- [I2C](./interface-interaction/i2c.md)

## Invasive Methods
These methods involve opening the device and physically interacting with the components on the board. These usually involve desoldering the component, rendering it unusable, unless perfectly reassebled.

Use these invasive methods only when non-invasive methods fail, and you have permission to "break" the device.

### Introduction to Chip Packages:
Knowing what chip you have on the device is essential to knowing which reader and extraction method you may or may not need to use when you are attempting to perform a chip-off extraction. A few of the most common package types are listed below

{% tabs %}
{% tab title="TSOP Package" %}
    TSOP (Thin Small Outline Package): A type of rectangular IC package where pins extend outward on both sides. It is commonly used for flash memory chips.

    different numbers ...
{% endtab %}

{% tab title="QFP Package" %}
    QFP (Quad Flat Package): A flat, square IC package with pins extending on all four sides, ideal for high-density chip designs.  

    different numbers ...
{% endtab %}

{% tab title="BGA Package" %}
    BGA (Ball Grid Array): A package type with connections in the form of solder balls on the underside of the chip, allowing for higher pin density but requiring specialized tools for handling.

    different numbers ...

{% endtab %}
{% endtabs %}



### Chip-Off Extraction of a QFP, TSOP, and Other Non-BGA Packages
Non-BGA packages are generally easier to interface with. They are more straightforward

### Chip-Off Extraction of a BGA-Package Flash Chip

### Chip-Off Extraction of UFS Flash in BGA Package