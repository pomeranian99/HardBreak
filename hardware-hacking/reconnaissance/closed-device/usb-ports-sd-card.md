# USB Ports / SD-card

In IoT devices, USB ports and SD card slots are commonly used for tasks such as firmware updates, data storage, and system configuration. USB ports often serve as an interface for connecting peripherals, debugging hardware, or performing maintenance tasks like resetting or updating the device's software. SD cards are frequently employed as storage media for logging sensor data, storing system configurations, or holding boot images, especially in embedded systems with limited onboard memory. These interfaces provide convenience and expandability but also introduce potential security risks if not properly secured, as they allow physical access to the device’s core functions.

## Usage

Check in the manual which functionality the USB-Port or SD-card might have:

* Updating firmware or applying patches to keep the device’s software current.
* Transferring data between the IoT device and external systems or peripherals.
* Facilitating debugging and diagnostics by providing access for troubleshooting tools.
* Connecting external peripherals like cameras, sensors, or keyboards to expand functionality.
* Enabling network access through a USB-to-Ethernet adapter when built-in Ethernet is unavailable.
* Connecting hardware security tokens or dongles for secure access or authentication.

How to analyze:

1. You should use USBPcap to intercept the data which is transferred over the USB port
   1. you could intercept a firmware update or other sensitive data
2. Can you try to manipulate the data?
   1. try change passwords etc.
3. Is the USB Port used as a COM Port?&#x20;
   1. Try to connect to it using Putty (Windows) or minicom(Linux)

## Firmware Updates

Firmware updates are especially interesting, since they contain all the code of the device. In manuals there is often a method described how to update the firmware of the IoT device over USB or SD. If the integrity of the firmware update is not checked, you can try to manipulate the update (for example changing passwords).

## Backup and Restore Functions

You should also check if there are backup or restore functionalities implemented. If you can back up the device's configuration to an USB stick / SD card, then you might extract sensitive information from it.

If you can restore the configuration from a file on a USB stick / SD card then you may manipulate sensitive data like passwords in the config. If the integrity of the restore file is not checked, the known passwords will then be used by the IoT device.



