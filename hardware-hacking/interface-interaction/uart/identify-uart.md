# Identify UART

This page should will teach you how to identify a UART interface. If you already confirmed the found debug connector is using UART you may continue with[ Connect to UART](connect-to-uart.md).

To interact with a UART interface, you would need:

* A multimeter
* an USB to UART TTL adapter
* jumper cables
* and in some cases: a soldering station

After opening the device follow:

1. **Get an overview of what is available of the PCB board**
   1. Checkout which chips are used&#x20;
      1. Google the datasheet of each chip you find (model should be printed on top of the chip)
      2.  It can be useful to take a picture of the PCB and label everything you can identify

          <figure><img src="../../../.gitbook/assets/komplett-beschriftet (1).png" alt="" width="375"><figcaption><p>Example layout of an PCB</p></figcaption></figure>
   2.  Check for connector or test pads

       1. For UART we need pins: TX,RX,GND often manufacturers also put a VCC pin next to power the device. So we are looking for 4 pads or pins on the PCB board, like here:

       <figure><img src="../../../.gitbook/assets/image.png" alt="" width="188"><figcaption><p>Potential UART pins</p></figcaption></figure>

       1. Even better if we find actual pins, where we can connect jumper cables to:

       <figure><img src="../../../.gitbook/assets/image (31).png" alt="" width="172"><figcaption><p>Uart pins exposed</p></figcaption></figure>
2.  **Check the pinout for the connectors:**

    1.  Put your multimeter in continuity mode (often a "sound" symbol):

        <figure><img src="../../../.gitbook/assets/image (6).png" alt="" width="338"><figcaption><p>Multimeter in continuity mode</p></figcaption></figure>
    2. This mode will check if there is a direct link between two points on the PCB
    3. Put one probe on the connector pad you want to test
    4.  The other one goes on the chip (its datasheet will tell you which pins are used for UART)

        <figure><img src="../../../.gitbook/assets/image (5).png" alt="" width="287"><figcaption><p>How to probe</p></figcaption></figure>

    You need to find the GND (ground), TX (transmit) and RX(receive) pins to communicate with UART.
3.  If you could identify all the needed pins, you may now [Connect to UART](connect-to-uart.md).

