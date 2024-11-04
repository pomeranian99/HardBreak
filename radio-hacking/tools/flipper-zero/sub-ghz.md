# Sub-GHz

The Flipper Zero is equipped with a built-in CC1101 transceiver that can receive and transmit radio frequencies between 300-928 MHz. It can read, store, and emulate signals from remote controls (like gates,remote switches, wireless doorbells, smart lighting, etc.).&#x20;

The Flipper Zero web page describes all the techniques in detail:  [https://docs.flipper.net/sub-ghz](https://docs.flipper.net/sub-ghz)

Here are some hints:

* If you don't know the frequency: Start with the Frequency Analyzer to determine it
* If you don't know the modulation: "Read Raw" and try to figure out the correct modulation used
* You need to configure the right modulation before reading a signal, else, Flipper Zero will not receive the correct data. Flipper supports:
  * AM270
  * AM650
  * FM238
  * FM476
