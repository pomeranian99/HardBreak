---
icon: circle-chevron-right
---

# Common Hardware Components

## **Common Hardware Components in IoT & Hardware Hacking**

When performing hardware hacking or analyzing IoT devices, it’s important to understand the basic components that make up the device. Below is a quick reference guide to common hardware components.

* **Capacitors**
  * _Function_: Store and release electrical energy. They help regulate voltage and filter noise in circuits.
  * _Relevance to Pentesters_: Capacitors can affect power analysis techniques, especially in side-channel attacks. They often need to be removed for that reason.
* **Flash Chips**
  * _Function_: Non-volatile memory used to store firmware and device settings.
  * _Relevance to Pentesters_: Flash chips often contain firmware that can be extracted and analyzed. Tools like a flash programmer can be used to read from flash chips.
* **RAM (Random Access Memory)**
  * _Function_: Temporary memory that stores data for quick access by the device’s processor.
  * _Relevance to Pentesters_: RAM often contains runtime data, and in some cases, sensitive information can be extracted for analysis, especially during volatile memory analysis in exploitation or reverse engineering.
* **MCU (Microcontroller Unit)**
  * _Function_: A small computer on a single integrated circuit containing a processor, memory, and I/O peripherals.
  * _Relevance to Pentesters_: MCUs control the behavior of embedded systems. By analyzing or reprogramming MCUs, pentesters can manipulate the behavior of IoT devices.
  * _Common MCUs_: STM32, ESP8266, LPC1768
* **Resistors**
  * _Function_: Limit or control the current flow in a circuit.
  * _Relevance to Pentesters_: Understanding resistor configurations helps in circuit analysis, especially in reverse engineering hardware designs.
* **Diodes**
  * _Function_: Allow current to flow in one direction while blocking it in the opposite direction.
  * _Relevance to Pentesters_: Diodes protect sensitive components from reverse voltage. Zener diodes, for example, regulate voltage in circuits, which is useful in power behavior analysis.
* **Transistors**
  * _Function_: Act as switches or amplifiers, controlling large amounts of current with small inputs.
  * _Relevance to Pentesters_: Transistors are found in almost every circuit. Understanding how they control signals is vital when analyzing or manipulating hardware circuits.
  * _Types_: Bipolar Junction Transistors (BJT), Field Effect Transistors (FET), Metal Oxide Semiconductor FETs (MOSFET)
* **EEPROM (Electrically Erasable Programmable Read-Only Memory)**
  * _Function_: Non-volatile memory used for storing small amounts of data, such as device configurations.
  * _Relevance to Pentesters_: EEPROMs may store critical configuration data that can be dumped for analysis or modified to change device behavior.
  * _Common Interfaces_: I2C, SPI
* **Crystals / Oscillators**
  * _Function_: Provide a clock signal to synchronize operations in digital circuits.
  * _Relevance to Pentesters_: Crystals are key in timing-related attacks, such as clock glitching. Precise timing manipulation can sometimes lead to exploitable conditions in embedded systems.
  * _Types_: Quartz crystals, ceramic resonators
* **Voltage Regulators**
  * _Function_: Maintain a constant voltage level for components in a circuit.
  * _Relevance to Pentesters_: Voltage regulators play a role in power analysis, especially during fault injection or brown-out attacks where system voltage stability is critical.
  * _Types_: Linear regulators (e.g., LM7805), switching regulators
* **LEDs (Light Emitting Diodes)**
  * _Function_: Emit light when current passes through them.
  * _Relevance to Pentesters_: LEDs provide visual feedback on the state of a device. They are also often used in optical communication or data transfer for debugging.
  * _Common Variants_: Standard LEDs, IR LEDs
* **Inductors**
  * _Function_: Store energy in a magnetic field when current passes through them.
  * _Relevance to Pentesters_: Inductors are important in power circuits and can affect power analysis attacks. They are often found in combination with capacitors in filters or oscillators.
* **Push Buttons / Switches**
  * _Function_: Allow manual control of circuits by opening or closing an electrical connection.
  * _Relevance to Pentesters_: Buttons or switches are common on IoT devices for user input or reset purposes. Manipulating them at the right time during the boot process could bypass security mechanisms.
* **Connectors (e.g., JTAG, UART, USB)**
  * _Function_: Provide a physical interface for communication between hardware devices or for debugging purposes.
  * _Relevance to Pentesters_: Connectors like JTAG and UART give direct access to the internal functioning of a device. Understanding these interfaces helps in gaining control over hardware or extracting sensitive data.
  * _Common Interfaces_: JTAG, UART, I2C, SPI
* **Jumpers**
  * _Function_: Small connectors used to manually set configurations or routes on a circuit board by connecting specific pins.
  * _Relevance to Pentesters_: Jumpers are often used to enable or disable features of a device, such as entering debug or boot modes. Adjusting jumpers can help pentesters gain access to restricted areas or manipulate boot settings.
* **eMMC (embedded MultiMediaCard)**
  * _Function_: Non-volatile memory used for mass storage in embedded systems. It combines flash memory and a controller in one package.
  * _Relevance to Pentesters_: eMMC is often used to store operating systems, firmware, or sensitive data in IoT devices, similar to SD cards. Pentesters may use eMMC readers to dump the contents for analysis, extracting valuable information such as passwords, encryption keys, or firmware.
