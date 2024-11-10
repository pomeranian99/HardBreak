# Parrot Anafi Drone Reverse Engineering

In this example, we demonstrate how we reverse-engineered the communication between the Parrot Anafi consumer drone and its controller, which connect via Wi-Fi. The Parrot Anafi hosts its own Wi-Fi network, allowing either the controller or a phone running the Freeflight app to connect. Our goal was to understand the signals sent to the Anafi for initiating takeoff and landing sequences.

Steps to analyze the signals:

1. Connect your PC to the Parrrot Anafi's WIFI network
2. To be able to capture all communication between the controller and the drone we have to perform an ARP-Spoofing attack to get a Man-in-the-middle position between the drone and it's controller. This can be done by using `ettercap` for example.
3.  The resulting test setup may look like this:

    <figure><img src="../../../../.gitbook/assets/image (75).png" alt=""><figcaption><p>Parrot Anafi test setup</p></figcaption></figure>
4.  With wireshark we can look at the packets, which are send during a landing and a starting sequence (picture shows just a snippet):

    <figure><img src="../../../../.gitbook/assets/image (11).png" alt=""><figcaption><p>Example packet</p></figcaption></figure>
5. We can see that the communication between the drone and the controller is done over UDP. Everey UDP packet had some kind of hex string as payload, which was non-ASCII
6.  Next, we looked at the distribution of the packets send, of all packets send during one start and landing of the drone:

    <figure><img src="../../../../.gitbook/assets/image (12).png" alt=""><figcaption><p>Distribution of UDP packet type during one start and landing</p></figcaption></figure>
7. To distinguish which paket is responsible for the start and landing we captured 17 start and landings and saw that the amount of third type (length=53 bytes) of messages went from 2 to 34. Could this be the packet which controls the start/landing? since 17\*2=34
8.  We can filter in Wireshark with `frame.len==53` to filter just for the start/landing packets

    <figure><img src="../../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>
9.  The payload of the packets had a pretty clear structure: (here an example of a few)

    ```
    04 0b 0b 00 00 00 00 01 00 01 00
    04 0b 0c 0b 00 00 00 01 00 03 00
    04 0b 0d 0b 00 00 00 01 00 01 00
    04 0b 0e 0b 00 00 00 01 00 03 00
    04 0b 0f 0b 00 00 00 01 00 01 00
    04 0b 10 0b 00 00 00 01 00 03 00
    04 0b 11 0b 00 00 00 01 00 01 00
    04 0b 12 0b 00 00 00 01 00 03 00
    ```
10. After analyzing the protocol more, we could reverse the format of this type packet:

    <figure><img src="../../../../.gitbook/assets/image (15).png" alt=""><figcaption><p>Structure of start and landing packets</p></figcaption></figure>
11. We setup a Python script to send the command `040bff0b000000300001000100` to the drone to start it. Note that we set the counter to `FF`, as packets are dropped by the drone if the counter value is less than the current counter. Using `FF` ensures it is always accepted.
12. And we did it! The drone performed its auto-start maneuver and was hovering above!
13. In order to land the drone again we can send `040bff0b000000300001000300`to the drone. Note that the trigger byte (2nd last byte) was set to `03`.
14. Notice, one does not need to change the MAC address to get these results. The Anafi processed the packages even though the laptop was not the primary controller at this time.
15. **Possible ATTACKS (only possible when connected to the Anafi's WIFI)**
    1. Prevent starts
       1. The next experiment was to spam the landing command constantly, with the result that the drone was unable to start using the controller. The drone’s rotors were spinning for a second but then the landing command was received and the Anafi stopped the starting process.
    2. Prevent landing
       1. The same result could be achieved with spamming the starting package. If one presses the landing button on the controller or phone the drone started to go down, but as soon as the starting package from the laptop came in the drone stopped the landing and stared to hovering above the ground again. As a result, the phone user was unable to land the drone properly.
16. This case study shows why it is relevant to reverse network protocols when analyzing IoT devices.

## Resources

Bachelor Thesis, Jonas Rosenberger

[https://www.parrot.com/en/drones/anafi](https://www.parrot.com/en/drones/anafi)
