# Network Traffic & Security Analysis Using Wireshark

## Project Objective
The goal of this project was to capture live network traffic over a standard Wi-Fi connection to analyse how core networking protocols operate and to identify potential privacy and security risks. 

By analysing raw data packets, this project simulates the fundamental monitoring and risk assessment tasks performed by a Security Operations Centre (SOC) Analyst.

---

## Tools Used
* **Network Protocol Analyzer:** Wireshark v4.6.5
* **Environment:** Live 802.11 Wi-Fi interface capture
* **Protocols Investigated:** DNS (Domain Name System), TCP (Transmission Control Protocol), HTTP (Hypertext Transfer Protocol)

---

## Key Findings & Analysis

### 1. Plain-Text Metadata Leakage via DNS
By applying the `dns` display filter, I isolated the domain name requests sent by my computer. 

* **Observation:** The capture caught plain-text requests for active services running on my machine, including `web.whatsapp.com`, `grammarly.com`, `adobe.io`, and academic portals (`aibi.instructure.com`). 
* **The Security Risk:** Even though the actual data sent to these websites is encrypted, standard **DNS queries are sent in cleartext**. An eavesdropper on the same network can track these queries to build a detailed profile of a user's habits, software assets, and school or work affiliations for targeted phishing attacks.

### 2. Internal Device Reconnaissance via HTTP (UPnP)
Using the `http` filter, I looked for any completely unencrypted application layer web traffic.

* **Observation:** I discovered heavy plain-text communication between internal network devices (`192.168.1.16` and `192.168.1.38`). The devices were utilizing Universal Plug and Play (UPnP) to exchange device configuration settings (`rendererdevicedesc.xml`) and multimedia icons over unencrypted HTTP.
* **The Security Risk:** Cleartext local protocols allow an attacker who has compromised one device on a Wi-Fi network to silently intercept local data streams, map out all active smart appliances, and plan lateral movement without running loud network scans.

### 3. Transport Layer Mechanics & Reliability via TCP
Using the specialized filter `tcp.flags.syn == 1`, I isolated the initialization of TCP connections.

* **Observation:** The capture successfully captured the standard TCP Three-Way Handshake sequence (`[SYN]` -> `[SYN, ACK]` -> `[ACK]`) used to open stable connections. It also highlighted `[TCP Retransmission]` errors, where the network automatically resent data packets that didn't receive a timely acknowledgment.
* **The Security Value:** Analyzing these handshakes and retransmissions demonstrates an understanding of network layer-4 reliability controls, which is vital for diagnosing connection bottlenecks or spotting Denial of Service (DoS) anomalies in a corporate environment.

---

## Recommended Security Mitigations

1. **Enable DNS over HTTPS (DoH):** Encrypting outbound DNS queries prevents local network sniffers from reading the website domains being resolved by the endpoint.
2. **Implement Network Segmentation:** Isolate local IoT, media servers, and UPnP devices onto an isolated guest network or VLAN to prevent lateral visibility from critical student or corporate workstations.
3. **Utilise a Virtual Private Network (VPN):** Encapsulating local link traffic ensures that plain-text local protocols remain completely hidden from other participants on a shared or untrusted network interface.

---

















## 🎯 Conclusion
This project demonstrates that standard network operations leave significant footprints by default. While payload data is largely protected by modern web encryption, metadata (DNS) and local discovery protocols (UPnP) remain exposed. Securing a modern environment requires extending encryption across every layer of the network architecture.
