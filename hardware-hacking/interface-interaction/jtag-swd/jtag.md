# JTAG

## **Theory**

JTAG (Joint Test Action Group) is a standard interface used for testing, debugging, and programming embedded systems, especially microcontrollers and FPGAs. JTAG is often used during development to diagnose hardware issues or to program devices in-system. It allows direct access to a device’s memory, registers, and other critical functions. For pentesters, exploiting JTAG can provide deep insights into a device’s internals, enabling you to extract firmware, bypass security mechanisms, or alter device behavior.

## **Requirements:**

1. Hardware
   * JTAG Adapter (e.g., Bus Pirate, Segger J-Link, FTDI-based adapters, or OpenOCD-compatible adapters)
   * Jumper wires to connect the JTAG adapter to the target device
   * Multimeter to check voltages and identify JTAG pins
   * Soldering kit (if JTAG pins are not exposed)
2. Software
   * OpenOCD (Open On-Chip Debugger) for JTAG interaction
   * UrJTAG (open-source JTAG tools)
   * GDB (GNU Debugger) for debugging over JTAG
   * J-Link software (for Segger J-Link adapters)
   * Binwalk (for firmware analysis after extraction)

## **Usage**

1.  Identifying JTAG Pins:

    * JTAG typically uses multiple pins, including:
      * TDI (Test Data In): Data input to the device.
      * TDO (Test Data Out): Data output from the device.
      * TCK (Test Clock): Clock signal for synchronization.
      * TMS (Test Mode Select): Mode selection signal.
      * TRST (Test Reset, optional): Resets the JTAG state machine.
    * Use a multimeter to check voltage levels on the JTAG header (typically 3.3V or 5V).

    Command Example (OpenOCD for Pin Identification):

    ```bash
    openocd -f interface/ftdi.cfg -f target/your_target.cfg -c "init; scan_chain; shutdown"
    ```

    This command initializes the connection to the JTAG chain and identifies connected devices.
2.  Device Discovery and JTAG Chain Scanning:

    * Once the JTAG pins are identified, the next step is to scan the JTAG chain to discover connected devices, such as microcontrollers or FPGAs.

    Command Example (JTAG Chain Scan with OpenOCD):

    ```bash
    openocd -f interface/jlink.cfg -f target/stm32f4x.cfg -c "init; scan_chain; shutdown"
    ```

    This scans the JTAG chain for devices connected to the bus.

    Command Example (UrJTAG Chain Scan):

    ```bash
    jtag> cable ft2232 pid=0x6010 vid=0x0403 interface=1
    jtag> detect
    ```

    This detects and lists JTAG devices connected to the FTDI-based adapter.
3.  Dumping Firmware via JTAG:

    * Once the target device is discovered, JTAG can be used to dump the firmware from the device’s memory. This is a crucial step in analyzing the system for vulnerabilities, backdoors, or sensitive information.

    Command Example (Dumping Memory via OpenOCD):

    ```bash
    openocd -f interface/jlink.cfg -f target/stm32f4x.cfg -c "init; dump_image firmware.bin 0x08000000 0x10000; shutdown"
    ```

    This dumps the firmware from memory address `0x08000000` to a file named `firmware.bin`.
4.  Modifying Firmware:

    * JTAG allows you to write directly to the device’s memory, including reprogramming the flash with modified firmware. This can be used to inject backdoors, modify settings, or tamper with system functions.

    Command Example (Flashing Firmware via OpenOCD):

    ```bash
    openocd -f interface/jlink.cfg -f target/stm32f4x.cfg -c "program modified_firmware.bin 0x08000000 verify reset exit"
    ```

    This writes the `modified_firmware.bin` file to the target device and verifies the changes.
5.  Debugging and Code Execution:

    * JTAG allows setting breakpoints and stepping through code, making it a powerful tool for debugging. You can halt execution, inspect memory, and control the flow of execution to analyze or bypass security mechanisms.

    Command Example (Attaching GDB to a JTAG Device):

    ```bash
    gdb-multiarch firmware.elf
    (gdb) target remote :3333
    (gdb) monitor reset halt
    (gdb) break main
    (gdb) continue
    ```

    This attaches GDB to the target device and sets a breakpoint at the `main` function.
6.  Bricking and Recovery:

    * JTAG is often the last resort for recovering bricked devices. If a device becomes non-functional due to a failed firmware update or configuration changes, JTAG can reflash the firmware or restore functionality.

    Command Example (Reflashing a Bricked Device via JTAG):

    ```bash
    openocd -f interface/jlink.cfg -f target/stm32f4x.cfg -c "program recovery_firmware.bin 0x08000000 verify reset exit"
    ```

    This reflashes a bricked STM32 device with recovery firmware.

## Resources

[https://hackaday.com/2020/04/08/a-hackers-guide-to-jtag/](https://hackaday.com/2020/04/08/a-hackers-guide-to-jtag/)\
[https://riverloopsecurity.com/blog/2021/05/hw-101-jtag/](https://riverloopsecurity.com/blog/2021/05/hw-101-jtag/)\
[http://dangerousprototypes.com/docs/Bus\_Blaster\_urJTAG\_guide](http://dangerousprototypes.com/docs/Bus\_Blaster\_urJTAG\_guide)
