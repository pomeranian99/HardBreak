# RF Signal Analyzers

## Theory

RF Signal Analyzers are essential tools for analyzing and measuring radio frequency (RF) signals, often used in wireless communication systems, IoT devices, and hardware security testing. They allow hardware pentesters to capture, analyze, and decode RF signals for reverse engineering, interference detection, or vulnerability exploitation.

Key concepts and functions:

* Frequency Spectrum
  * RF signal analyzers scan and visualize signals over a range of frequencies, typically between a few kHz and several GHz, depending on the device's capabilities.
* Modulation
  * RF signals are often modulated, meaning that they carry information using various modulation schemes like AM, FM, QAM, etc. Analyzers decode these modulations to interpret the transmitted data.
* Spectrum Analysis
  * They use a superheterodyne receiver to mix incoming signals with a known local oscillator signal, allowing the device to display frequency content and power levels in real-time.

## Usage

* Signal Capture
  * RF signal analyzers capture and measure wireless signals, such as Wi-Fi, Bluetooth, Zigbee, and other RF communication protocols.
* Frequency Analysis
  * These tools measure frequency, bandwidth, modulation, and power levels of RF signals, providing valuable insight into communication patterns.
* Reverse Engineering
  * RF analyzers are used to reverse engineer proprietary RF protocols, allowing for potential exploitation or testing of wireless vulnerabilities.
* Interference Detection
  * They help detect unwanted signals or interference that may disrupt or compromise communication.

## Models:

* Entry-Level
  * RTL-SDR(<$15) : supports sub 1 GHZ signals, can only record not send
* Mid-Range
  * Flipper Zero ($200): RF capabilities (capture and send), including RFID and NFC testing
* High-End
  * HackRF One ($350): supports wide range of radio signals
