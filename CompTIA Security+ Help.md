# CompTIA Security+ Help

## Hashing Vs. Encryption

https://nordvpn.com/blog/hashing-vs-encryption/

## Slightly redundant hashing information

https://nordvpn.com/cybersecurity/glossary/hashing/

## Table Of Contents

1. [String](#string)
1. [Hash](#hash)
1. [Encryption](#encryption)
1. [CRC](#crc)
1. [Network Architecture](#network-architecture)
    1. [Network Topologies](#network-topologies)
    1. [Network Components](#network-components)
    1. [Network Protocols](#network-protocols)
    1. [Network Security Concepts](#network-security-concepts)
    1. [Additional Topics](#additional-topics)

### String

Text (a "string" of characters. Think of it like that Christmas shit where you string popcorn on a thread, where each piece of popcorn is a character)

### Hash

One-way conversion of text to a fixed length cipher (always the same length, so `SHA256` outputs `32` characters (`256 / 8`))

### Encryption

You already know what that is

### CRC

(Cyclic Redundancy Check); Like a hash, but super duper fast and usually used for data communication

Hash Collision = When data that is slightly or completely different produces the same hash. Like when `1+1+1+1 = 4`, but so does `2+2`, or `1+3`, etc.

[Example Of CRC](#crc-example)

---

## Network Architecture

**Network architecture** is a fundamental concept in Security+. It refers to the design and structure of a network, including its components, topology, and protocols. Here are key aspects to include in your Markdown file:

---

### Network Topologies

-   **Bus Topology:** A simple, linear arrangement where all devices are connected to a single cable.
-   **Star Topology:** A central device (hub or switch) connects all other devices.
-   **Ring Topology:** Devices are connected in a circular fashion, with each device acting as a repeater.
-   **Mesh Topology:** Every device is connected directly to every other device.
-   **Hybrid Topology:** A combination of two or more topologies.

---

### Network Components

-   **Routers:** Devices that connect networks and determine the best path for data.
-   **Switches:** Devices that connect devices within a network.
-   **Hubs:** Simple devices that broadcast data to all connected devices.
-   **Firewalls:** Devices that filter network traffic to protect against unauthorized access.
-   **Intrusion Detection Systems (IDS):** Monitor network traffic for suspicious activity.
-   **Intrusion Prevention Systems (IPS):** Actively block attacks.

---

### Network Protocols

-   **TCP/IP:** The foundation of the internet, consisting of TCP (Transmission Control Protocol) for reliable data transfer and IP (Internet Protocol) for addressing and routing.

    -   **TCP Port Numbers:**
        -   **80:** HTTP (Hypertext Transfer Protocol)
        -   **443:** HTTPS (Hypertext Transfer Protocol Secure)
        -   **22:** SSH (Secure Shell)
        -   **23:** Telnet
        -   **25:** SMTP (Simple Mail Transfer Protocol)
        -   **21:** FTP (File Transfer Protocol)
        -   **20:** FTP Data Transfer
            -   This port is used for transfering the data, **21** is used for communication for setting up and maintaining the transfer. Like the control tower at an airport.
    -   **UDP Port Numbers:**

        -   **53:** DNS (Domain Name System, Converts domains to IP addresses)
            -   *Example:* When navigating to Google, a DNS will take `google.com` and return `142.250.72.238`. Then your computer will talk to the computer using that returned IP.
        -   **67/68:** DHCP (Dynamic Host Configuration Protocol)
            -   Issues and manages IP addresses (Our ASUS router hosts this; Your phone get's it's local IP via this service when connecting to `RBHE-XXX`)
        -   **123:** NTP (Network Time Protocol)
            -   Keeps computer clocks synchronized
        -   **137/138/139/140:** NetBIOS (Network Basic Input/Output System)

    -   **_TCP Vs. UDP_**

        -   **TCP (Transmission Control Protocol):**

            -   **Reliable:** Like sending a package with tracking. You can be sure it will arrive safely and in the right order.
            -   **Slow:** Takes longer to send data because it's checking everything.
            -   **Good for:** Important data like emails or downloading files.

        -   **UDP (User Datagram Protocol):**

            -   **Unreliable:** Like sending a postcard. It might get lost or arrive out of order.
            -   **Fast:** Sends data quickly without checking everything.
            -   **Good for:** Things that don't need to be perfect, like streaming videos or online games.

-   **HTTP:** Used for transferring web pages.

    -   **Port 80:** Standard HTTP
    -   **Port 443:** HTTPS (secure HTTP)

-   **HTTPS:** A secure version of HTTP that uses encryption.

    -   **Port 443**

-   **FTP:** Used for transferring files.

    -   **Port 21:** Control connection
    -   **Port 20:** Data connection

-   **SMTP:** Used for sending emails.

    -   **Port 25:** Standard SMTP
    -   **Port 587:** Submission port for SMTP

-   **POP3 and IMAP:** Used for receiving emails.
    -   **POP3:** (Post Office Protocol) Port `110` (standard) or `995` (SSL/TLS)
    -   **IMAP:** (Internet Message Access Protocol) Port `143` (standard) or `993` (SSL/TLS)

**Note:** These are common port numbers, but organizations can customize them. It's essential to be aware of any deviations from the standard port numbers in your specific network environment.

---

### Network Security Concepts

-   **VLANs:** Virtual Local Area Networks that allow logical segmentation of a physical network.
-   **DMZ:** A demilitarized zone that acts as a buffer between a trusted internal network and an untrusted external network.
-   **VPN:** A Virtual Private Network that creates a secure tunnel over an untrusted network.
-   **NAT:** Network Address Translation that allows multiple devices to share a single public IP address.

---

### Additional Topics

-   **Network Segmentation:** Dividing a network into smaller, more manageable segments.
-   **Network Monitoring:** Using tools to monitor network performance and identify potential issues.
-   **Network Troubleshooting:** Techniques for diagnosing and resolving network problems.

---

## CRC Example

Example of CRC:
I have to send this list of numbers to a friend

```C#
    234
    4992
    480
    5920
    4302
    5093842
    9293
    939
    420
    69
```

To ensure corruption doesn't happen during transport, I could have my friend relay this entire list back to me to ensure it's successful. However, that's super wasteful for bandwidth and time. So instead, I'll send over a CRC.
This CRC is all values in the list added up. The CRC I'll give is `5120491` (`5,120,491`)

That's how a CRC is similar to a hash. It's non-reversible. It's an amalgamation of the data, and you wouldn't even know where to begin with deconstructing it.
How many different numbers went into adding up to `5,120,491`? Are any of them negative? All these factors make it impossible to reverse a hash. That's why brute-forcing hashes is the most reliable way of cracking them.
