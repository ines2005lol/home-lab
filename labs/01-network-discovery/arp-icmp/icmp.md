# ICMP (Internet Control Message Protocol)

## Objective

The purpose of this section is to understand how devices use ICMP to test network connectivity and exchange control messages.

## What is ICMP?

ICMP (Internet Control Message Protocol) is a network layer protocol used by devices to send error messages and diagnostic information about network communication.

Unlike protocols such as TCP or UDP, ICMP does not transport application data. Instead, it helps devices determine whether another host is reachable and provides information about network problems.

The most common use of ICMP is the `ping` command, which sends an ICMP Echo Request to a target device. If the target is reachable, it responds with an ICMP Echo Reply.

## Why is ICMP Important?

* Tests network connectivity between devices.
* Helps troubleshoot network problems.
* Provides diagnostic information.
* Used by tools such as `ping` and `traceroute`.
* Helps identify packet loss and latency issues.

# Connectivity Testing

## Objective

Verify that both virtual machines can communicate over the Internal Network.

### Windows → Kali

<img width="457" height="197" alt="image" src="https://github.com/user-attachments/assets/e24156a0-666f-45eb-b32e-e9767a3ecaeb" />

### Kali → Windows

<img width="527" height="177" alt="image" src="https://github.com/user-attachments/assets/d16c88a1-02a6-4a54-a82c-a413c7e9531f" />

## Result

Both systems successfully exchanged ICMP echo requests and replies, confirming that the network configuration was functioning correctly.

## Security Considerations

ICMP can also be used by attackers for reconnaissance and network discovery.

Examples:

* Discovering active hosts using ping sweeps.
* Performing denial-of-service attacks using excessive ICMP traffic.

Because of this, many networks monitor or restrict unnecessary ICMP traffic.

