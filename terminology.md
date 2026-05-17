# Network Analysis Glossary & Core Terminologies

This document defines the fundamental networking and cybersecurity terms utilized throughout this traffic analysis project. Understanding these concepts is essential for interpreting raw packet streams and identifying structural vulnerabilities.

---

## 1. Infrastructure & Interface Terms

### Network Interface Card (NIC)
The physical hardware component (such as a Wi-Fi card or an Ethernet adapter) that allows a computer to connect to a local network. In this project, the live wireless network adapter was selected as the interface to capture over-the-air packet frames.

### Packet
The basic unit of data transmitted over a network. When data is sent (such as a webpage loading or a message sending), the protocol stacks chop the information into thousands of small, structured blocks called packets. These are transmitted independently and reassembled perfectly at the destination endpoint.

### Private vs. Public IP Addresses
* **Private IP Address (e.g., `192.168.1.x`):** Local network coordinates assigned by an internal router. These addresses are unique inside the home or office network but cannot be reached directly from the public internet.
* **Public IP Address:** The external facing identity assigned to a local network gateway by an Internet Service Provider (ISP). All internet-bound traffic exits the network under this singular public routing identity.

---

## 2. Application Layer Protocols

### Domain Name System (DNS)
Often referred to as the "Phonebook of the Internet," DNS translates human-readable web addresses (like `web.whatsapp.com`) into numerical IP addresses (like `157.240.2.34`) that networking equipment can actually route. 

### Cleartext (Plaintext)
Data that is transmitted or stored without cryptographic encryption. Cleartext data can be instantly read by anyone who intercepts it using basic packet sniffer configurations.

### Hypertext Transfer Protocol (HTTP)
The foundational, unencrypted application protocol used for transmitting web data across the internet. Because HTTP lacks encryption, all application payloads, request URIs, and structural metadata pass across the wire in cleartext.

### Universal Plug and Play (UPnP)
A set of networking protocols that permits local network devices (such as smart TVs, mobile applications, and media servers) to seamlessly discover each other's presence and establish functional connections automatically without requiring manual configuration.

---

## 3. Transport Layer Protocol Mechanics

### Transmission Control Protocol (TCP)
A connection-oriented, highly reliable transport protocol operating at Layer 4 of the OSI model. TCP ensures absolute data delivery by tracking packet sequences, managing traffic flow speeds, and verifying that every single packet is accounted for via explicit confirmations.

### TCP Three-Way Handshake
The mandatory initialization sequence TCP relies on to establish a verified, synchronized connection between a client machine and a remote host before transmitting real data payloads.
1. **SYN (Synchronize):** The client sends a synchronization packet request to initiate a connection session.
2. **SYN-ACK (Synchronize-Acknowledge):** The server returns a packet acknowledging the initial request and syncs its own parameters.
3. **ACK (Acknowledge):** The client acknowledges the server's parameters, finalizing the active TCP socket connection.

### TCP Retransmission
A self-healing structural protocol event. When an endpoint transmits a TCP packet, it initiates an internal timer. If the sender does not receive an acknowledgment (`ACK`) packet from the destination before the timer runs out, it assumes the packet was lost or dropped during transmission and automatically re-sends a duplicate copy.
