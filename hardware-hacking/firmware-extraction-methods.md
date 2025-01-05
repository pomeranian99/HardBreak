# Firmware Extraction Methods
Firmware is the software embedded in a device's hardware, often critical for its operation. Extracting and analyzing it is crucial to gain an insight into the device and establish a foothold by analysing, through methods of reverse engineering, or modifying the firmware and reflashing a device.

But before you can start analyzing, reversing and establishing your foothold, you first need to obtain the firmware itself.

Obtaining the firmware from devices can be done in several different ways.  Depending on the target device, firmware can be extracted through physical, semi-physical, or software-only methods. This page covers both invasive and non-invasive approaches.

## Non-Invasive Methods

These methods do not involve opening or physically tampering with the device and are often less risky.

### Downloading from the Manufacturer Website
Manufacturers often host firmware files on their official websites for manual updates.

*ToDo*

### MitM Attack on the Update Process
Many devices update their firmware via OTA updates. Capturing these updates can provide the firmware file.

*ToDo*

### Dumping Firmware through a Vulnerability
Exploiting a vulnerability in the device’s software or configuration to access and dump firmware.

*ToDo*

## Semi-Invasive Methods
These approaches require minimal physical interaction with the device but stop short of full disassembly.

### Exposed interfaces 

- [UART](./interface-interaction/uart/extract-firmware-using-uart.md)
- [SPI](./interface-interaction/spi/extract-firmware-using-spi.md)
- [JTAG/SWD](./interface-interaction/jtag-swd/extract-firmware-using-jtag-swd.md)
- [I2C](./interface-interaction/i2c.md)

## Invasive Methods
These methods involve opening the device and physically interacting with the components on the board. These usually involve desoldering the component, rendering it unusable, unless perfectly reassebled.

Use these invasive ,ethods only when non-invasive methods fail.

### Chip-Off Extraction of a QFP, TSOP, and Other Non-BGA Packages

### Chip-Off Extraction of a BGA-Package Flash Chip

### Chip-Off Extraction of UFS Flash in BGA Package