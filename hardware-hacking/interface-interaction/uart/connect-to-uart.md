# Connect to UART

## **Scenario:**&#x20;

You followed "Board Analysis" and could identify an active UART interface

## Connect to UART

You need to find the GND (ground), TX (transmit) and RX(receive) pins to communicate with UART.&#x20;

When you connect the UART-USB adapter with the UART interface on the board, you have to connect RX and TX together like this:

<figure><img src="../../../.gitbook/assets/image (8).png" alt=""><figcaption><p>Connect RX to TX and TX to RX</p></figcaption></figure>

There are different ways to connect to identified test pads:

* Soldering jumper cables directly on the board (takes time, but avoids lose connection)
* Using needle probes
* Soldering to the pads, Example:

<figure><img src="../../../.gitbook/assets/image (68).png" alt="" width="259"><figcaption><p>Soldered cables to UART pads</p></figcaption></figure>

## Interact with UART

On your PC use the following command to communicate over UART (you may have to adjust the baud rate)

{% tabs %}
{% tab title="Linux" %}
```bash
sudo minicom -D /dev/ttyUSB0 -b 115200
sudo picocom -b 115200 -r -l /dev/ttyUSB0
```
{% endtab %}

{% tab title="Windows" %}
**Using PuTTY (Windows)**:

* Select “Serial” and enter the COM port (e.g., COM3) and baud rate (115200).
{% endtab %}
{% endtabs %}

5. If you see readable data: You done it correctly!

<figure><img src="../../../.gitbook/assets/image (20).png" alt=""><figcaption><p>Bootlog</p></figcaption></figure>

**Congrats!** You found your first serial connection! Check out the UART chapter on how to use this to dump the firmware from the device.
