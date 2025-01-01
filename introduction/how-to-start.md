---
icon: flag-checkered
---

# How to start

In this chapter we want to describe on how to get started with hardware hacking and the tools you may need. Hardware hacking is all about investigating, breaking down, and understanding the underlying components of everyday devices—unlocking their secrets and sometimes even repurposing them for new tasks.

## Choosing Your First Target Device

To start hardware hacking, choose an old, expendable device as your first target. Avoid experimenting on valuable devices like your brother's PS5, as they are likely well-secured and could lead to frustration if something goes wrong. Hardware hacking can damage your device, so it's best to use something you don't mind breaking. A used or outdated router is an excellent option for beginners, as it offers components to analyze and often runs a Linux-based OS. Other potential targets include network switches, IP cameras, or any device with logic and internet connectivity.

#### Why Start with Old Devices?

* Less Risk
  * With old or broken devices, there’s no risk of breaking something essential.
* Affordability
  * You can find inexpensive or even free outdated routers, cameras, or other IoT devices.
* Less Secure
  * Many older devices use proprietary protocols that you might not encounter on modern hardware. This can provide valuable experience for recognizing and adapting to similar challenges on newer devices. Also, older and cheaper devices are most likely not very secure, so they are a good starting point to gain experience.

### Essential Tools for Hardware Hacking

Once you have your target device, you’ll need a few basic tools to get started. Hardware hacking often involves opening up devices, probing circuits, and sometimes connecting to hidden communication interfaces. Here’s a starter list:

#### 1. Screwdriver Set

Most devices are assembled with screws, so a set of small precision screwdrivers is essential. Look for a set that includes a variety of sizes and types, like Phillips and flathead, as you'll encounter different types of screws across devices.

#### 2. [Soldering Iron and Equipment](../hardware-hacking/basics/tools/hardware-tools/soldering-tools.md)

A soldering iron is crucial for attaching wires or replacing components. In hardware hacking, you'll often use it to attach wires to test points or UART (Universal Asynchronous Receiver-Transmitter) pins. Choose a soldering iron with adjustable temperature control, and get some basic soldering accessories like:

* Solder
  * Standard lead-free solder.
* Soldering Stand
  * Keeps the hot iron safely in place.
* Desoldering Pump/Wick
  * For removing solder, helpful if you make a mistake or need to free up a component.
* Soldering mat
  * to protect your table, in case solder drops down

#### 3. [Multimeter](../hardware-hacking/basics/tools/hardware-tools/multimeters-and-oscilloscopes.md)

A multimeter helps you measure voltage, resistance, and continuity, which is essential for checking connections and understanding the electrical characteristics of your target device. A good multimeter can prevent accidental shorts by helping you identify where power runs through the device.

#### 4. Jumper Cables

Jumper cables are useful for connecting different points on a circuit board without needing to solder, which is especially handy for quick testing. They're essential for connecting components like a UART adapter or power source temporarily.

#### 5. [UART Adapter](../hardware-hacking/basics/tools/hardware-tools/uart-to-ttl-adapter.md)

A UART (Universal Asynchronous Receiver-Transmitter) adapter allows you to communicate with the device’s serial interface. Many embedded systems, including routers, expose UART pins, which can provide a low-level console output. Through this connection, you may be able to access the device’s debug information or even drop into a root shell if it’s unsecured. A basic USB-to-UART adapter will allow you to connect the target device to your computer and start investigating.

#### 6. (Optional) [Bus Pirate](../hardware-hacking/basics/tools/hardware-tools/open-source-tools/bus-pirate.md)

The Bus Pirate is a versatile, open-source tool that can communicate with a wide range of protocols beyond UART. It’s especially useful for hardware hackers working with devices that use protocols like SPI (Serial Peripheral Interface), I²C (Inter-Integrated Circuit), and JTAG. Your chosen target device may not have an UART port, so you might have to look into alternative ways on how to dump its firmware. Although it’s optional, the Bus Pirate is a valuable addition to a hardware hacking toolkit if you plan to explore multiple protocols.

## Next Steps

Once you have your tools and target device, your next steps involve disassembling the device, locating debug interfaces like UART or JTAG (Joint Test Action Group), and analyzing its circuits. You'll get familiar with testing voltages, identifying data lines, and sometimes even dumping firmware to examine its contents.

I recommend reading the following pages on how to approach your first hardware hacking journey:

1. [Methodology](quickstart.md)
   1. Here we describe a general methodology on how to approach hardware hacking
2. [Reconnaissance](../network-analysis/reconnaissance.md)
   1. In this section we give an overview on what to look out for on a device
3. [Interface Interaction](../hardware-hacking/interface-interaction/)
   1. You found and interesting chip or connector on the device? This section will explain standard protocols like UART, SPI, JTAG etc. and how we can interact with them&#x20;
4. [Analyze Firmware](../hardware-hacking/analyze-firmware.md)
   1. You were able to dump the firmware? NICE WORK! Now it's time to analyze it, this section shows you what to do
5. You want to take different approaches? Check out [Network Analysis](../network-analysis/introduction.md) or [Radio Hacking](../radio-hacking/introduction.md)
6. [Contribute](../contribute/how-to-contribute.md)
   1. You may have come across a new proprietary protocol? Or you want to share the story on how you hacked your device? We would love to hear about it! This section will give you guidance on how you can support the hardware hacking community!

Hardware hacking requires patience and persistence, but with the right approach, you can uncover fascinating aspects of how these devices work.

