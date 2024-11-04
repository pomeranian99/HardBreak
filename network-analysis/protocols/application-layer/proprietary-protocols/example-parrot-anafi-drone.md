# Example: Parrot Anafi Drone

In this example we explain how we reversed the communication between the Parrot Anafi (consumer drone) and its controller, which communicate over WIFI.

Steps:

1. Connect your PC to the Parrrot Anafi's WIFInetwork
2. To be able to capture all communication between the controller and the drone we have to perform an ARP-Spoofing attack to get a Man-in-the-middle position. This can be done by using `ettercap` for example.
3.  With wireshark we can look at the packets, which are send:

    <figure><img src="../../../../.gitbook/assets/image (11).png" alt=""><figcaption><p>Example packet</p></figcaption></figure>
4. We can see that some kind of hex string over UDP is send, which is non-ascii
5.  Next, we looked at the distribution of the packets send, of all packets send during one start and landing of the drone

    <figure><img src="../../../../.gitbook/assets/image (12).png" alt=""><figcaption><p>Distribution of UDP packet type during one start and landing</p></figcaption></figure>
6. Next. we captured 17 start and landings and saw that the amount of third type of messages went from 2 to 34. Could this be the packet which controls the start/landing? since 17\*2=34
7.  We can now filter in Wireshark with `frame.len==53` to filter just for the start/landing packets

    <figure><img src="../../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>
8.  The payload of the packets had a pretty clear structure: (here an example of a few)

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
9.  After analyzing the protocol more, we could reverse the format of this type packet:

    <figure><img src="../../../../.gitbook/assets/image (15).png" alt=""><figcaption><p>Structure of start and landing packets</p></figcaption></figure>
10. We setup a Python script to send the command `040bff0b000000300001000100` to the drone to start it. Note that we set the counter to `FF`, as packets are dropped by the drone if the counter value is less than the current counter. Using `FF` ensures it is always accepted.
11. And we did it! The drone performed its auto-start maneuver and was hovering above!
12. In order to land the drone again we can send `040bff0b000000300001000300`to the drone.
13. Notice, one does not need to change the MAC address to get these results. The Anafi processed the packages even though the laptop was not the primary controller at this time.
14. **ATTACK (only possible when connected to the Anafi's WIFI)**
    1. Prevent starts
       1. The next experiment was to spam the landing command constantly, with the result that the drone was unable to start using the controller. The drone’s rotors were spinning for a second but then the landing command was received and the Anafi stopped the starting process.
    2. Prevent landing
       1. The same result could be achieved with spamming the starting package. If one presses the landing button on the controller or phone the drone started to go down, but as soon as the starting package from the laptop came in the drone stopped the landing and stared to hovering above the ground again. As a result, the phone user was unable to land the drone properly.
15. This case study shows why it is relevant to reverse network protocols when analyzing IoT devices.

## Resources

Bachelor Thesis, Jonas Rosenberger

[https://www.parrot.com/en/drones/anafi](https://www.parrot.com/en/drones/anafi)
