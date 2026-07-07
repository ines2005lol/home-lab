# ARP (Address Resolution Protocol)

## Objective

The purpose of this section is to understand how devices on the same local network discover each other's physical (MAC) addresses before exchanging data.

---

## What is ARP?

**ARP (Address Resolution Protocol)** is a network protocol that maps an IPv4 address to a device's **MAC (Media Access Control) address** on a local network.

When a device wants to communicate with another device on the same subnet, it first checks its ARP cache. 
If the MAC address is unknown, it broadcasts an ARP Request asking, "Who has this IP address?" The device with that IP responds with its MAC address, and the mapping is stored in the ARP cache for future use.

---

## Why is ARP Important?

* Enables communication between devices on the same local network.
* Translates IP addresses into MAC addresses.
* Reduces network traffic by caching previously learned mappings.
* Essential for Ethernet-based communication.

---

## Viewing the ARP Table

### Windows

<img width="432" height="165" alt="image" src="https://github.com/user-attachments/assets/d6bdf9cb-5a5d-42ac-8275-cf47d820a2ec" />

✎ dynamic: learned via ARP, expires over time.
✎ static: fixed/reserved entries (broadcast + well-known multicast groups), always present regardless of actual traffic.

### Kali Linux

<img width="472" height="67" alt="image" src="https://github.com/user-attachments/assets/d7965f55-1dca-4162-a798-5a32a0b7107a" />

✎ Windows' arp -a includes static broadcast/multicast entries as reference info. 
✎ Linux's ARP/neighbor table only lists dynamically-learned unicast mappings, since broadcast and multicast MACs are computed algorithmically and never require an ARP lookup — so they simply don't appear.

## Security Considerations

ARP does not verify the authenticity of responses, making it vulnerable to **ARP spoofing (ARP poisoning)** attacks. An attacker can send forged ARP replies to associate their own MAC address with another device's IP address, potentially enabling traffic interception or man-in-the-middle attacks.

---

## Key Takeaways

* ARP translates IPv4 addresses into MAC addresses.
* ARP operates only within a local network.
* Devices maintain an ARP cache to improve efficiency.
* Tools such as `arp`, `ip neigh`, `nmap`, and Wireshark can be used to inspect ARP information.
* Understanding ARP is fundamental for troubleshooting networks and performing security assessments.
