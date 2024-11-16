# Essential Tools

Once you have your target device, you’ll need a few basic tools to get started. Hardware hacking often involves opening up devices, probing circuits, and sometimes connecting to hidden communication interfaces. Here’s a starter list:

**1. Screwdriver Set**

Most devices are assembled with screws, so a set of small precision screwdrivers is essential. Look for a set that includes a variety of sizes and types, like Phillips and flathead, as you'll encounter different types of screws across devices.

**2.** [**Soldering Iron and Equipment**](https://www.hardbreak.wiki/hardware-hacking/basics/tools/hardware-tools/soldering-tools)

A soldering iron is crucial for attaching wires or replacing components. In hardware hacking, you'll often use it to attach wires to test points or UART (Universal Asynchronous Receiver-Transmitter) pins. Choose a soldering iron with adjustable temperature control, and get some basic soldering accessories like:

* Solder
  * Standard lead-free solder.
* Soldering Stand
  * Keeps the hot iron safely in place.
* Desoldering Pump/Wick
  * For removing solder, helpful if you make a mistake or need to free up a component.
* Soldering mat
  * to protect your table, in case solder drops down

**3.** [**Multimeter**](https://www.hardbreak.wiki/hardware-hacking/basics/tools/hardware-tools/multimeters-and-oscilloscopes)

A multimeter helps you measure voltage, resistance, and continuity, which is essential for checking connections and understanding the electrical characteristics of your target device. A good multimeter can prevent accidental shorts by helping you identify where power runs through the device.

**4. Jumper Cables**

Jumper cables are useful for connecting different points on a circuit board without needing to solder, which is especially handy for quick testing. They're essential for connecting components like a UART adapter or power source temporarily.

**5.** [**UART Adapter**](https://www.hardbreak.wiki/hardware-hacking/basics/tools/hardware-tools/uart-to-ttl-adapter)

A UART (Universal Asynchronous Receiver-Transmitter) adapter allows you to communicate with the device’s serial interface. Many embedded systems, including routers, expose UART pins, which can provide a low-level console output. Through this connection, you may be able to access the device’s debug information or even drop into a root shell if it’s unsecured. A basic USB-to-UART adapter will allow you to connect the target device to your computer and start investigating.

## Optional Tools, but usefull

Once you achieved your first firmware dump using UART and got hooked to hardware hacking, you may ask: what to get next?

**1.**  [**Bus Pirate**](https://www.hardbreak.wiki/hardware-hacking/basics/tools/hardware-tools/open-source-tools/bus-pirate)

The Bus Pirate is a versatile, open-source tool that can communicate with a wide range of protocols beyond UART. It’s especially useful for hardware hackers working with devices that use protocols like SPI (Serial Peripheral Interface), I²C (Inter-Integrated Circuit), and JTAG. Your chosen target device may not have an UART port, so you might have to look into alternative ways on how to dump its firmware. Although it’s optional, the Bus Pirate is a valuable addition to a hardware hacking toolkit if you plan to explore multiple protocols.

2. [Logic Analyzer](logic-analyzer/)

PCBs often feature pads or communication lines that are difficult to identify. A logic analyzer is a useful tool for identifying unknown interfaces and analyzing communication. Budget-friendly models are available for as little as $10-$15 and can handle basic analysis. For more advanced work, high-performance logic analyzers like the[ Saleae ](logic-analyzer/saleae-logic-analyzer.md)are pricier but offer powerful features that can decode a wide range of protocols.
