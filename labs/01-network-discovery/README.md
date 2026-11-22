# Lab 01 – Network Discovery

## Objective

This lab focuses on discovering hosts and services within an isolated virtual network using basic networking tools and Nmap, and on understanding what those tools actually send on the wire by capturing the traffic in Wireshark.

| Machine    | Role                      | IP Address    |
| ---------- | ------------------------- | ------------- |
| Kali Linux | Attacker / packet capture | 192.168.56.10 |
| Windows 10 | Target                    | 192.168.56.20 |

## Goals

* Configure and verify communication between virtual machines.
* Test connectivity using ICMP.
* Understand ARP and MAC addresses.
* Discover live hosts.
* Enumerate services running on a Windows machine.
* Compare TCP and UDP scanning techniques at the packet level.
* Document findings in a professional format.

## Contents

Recommended reading order:

| # | File | What it covers |
| - | ---- | -------------- |
| 1 | [setup.md](setup.md) | Lab environment and IP configuration |
| 2 | [arp-icmp/icmp.md](arp-icmp/icmp.md) | ICMP and ping connectivity testing |
| 3 | [arp-icmp/arp.md](arp-icmp/arp.md) | ARP and the ARP table on Windows vs Linux |
| 4 | [arp-icmp/wireshark.md](arp-icmp/wireshark.md) | Capturing ARP and ICMP traffic in Wireshark |
| 5 | [nmap-intro/nmap.md](nmap-intro/nmap.md) | Host discovery, port scanning, service and OS detection |
| 6 | [nmap-intro/notes.md](nmap-intro/notes.md) | Nmap options cheat sheet |
| 7 | [tcp-udp/README.md](tcp-udp/README.md) | TCP vs UDP theory |
| 8 | [tcp-udp/tcp-wireshark.md](tcp-udp/tcp-wireshark.md) | TCP Connect, SYN and ACK scans in Wireshark |
| 9 | [tcp-udp/udp-wireshark.md](tcp-udp/udp-wireshark.md) | UDP scanning with a Netcat listener |
| 10 | [findings.md](findings.md) | **Findings report**: results, risk and recommendations |

## Tools

`ping`, `arp`, `ip neigh`, Nmap, Wireshark, Netcat, Windows Defender Firewall
