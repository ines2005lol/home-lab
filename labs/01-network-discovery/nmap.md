# Nmap Network Scanning Lab

## Objective

The purpose of this section is to understand how Nmap can be used to discover hosts, identify open ports, and gather information about devices on a network.

This lab demonstrates:

* Host discovery
* Port scanning
* Service identification
* Basic network reconnaissance

## What is Nmap?

Nmap (Network Mapper) is a network scanning tool used to discover devices and services on a network.

It helps security professionals understand:

* Which hosts are active
* Which ports are open
* What services are running
* Potential security risks

## Lab Environment

| Machine       | Operating System | Role    |
| ------------- | ---------------- | ------- |
| Kali Linux VM | Linux            | Scanner |
| Windows VM    | Windows          | Target  |

Both machines are connected to the same internal network.

# Windows Firewall Configuration

## Objective

Before scanning, Windows Firewall rules were modified to allow Nmap to identify available ports and services.
Windows Firewall can block incoming connections, causing ports to appear as filtered during scanning.
The firewall was temporarily disabled using:

```cmd
netsh advfirewall set allprofiles state off
```

After disabling the firewall, Nmap was able to detect available ports more accurately.

> Note: This was performed only inside an isolated home lab environment.

To re-enable Windows Firewall after testing:

```cmd
netsh advfirewall set allprofiles state on
```

---

# Installation

Check if Nmap is installed:

```bash
nmap --version
```

If not installed:

```bash
sudo apt update
sudo apt install nmap
```

---

# Host Discovery

Before scanning ports, check if a device is reachable.

<img width="540" height="131" alt="image" src="https://github.com/user-attachments/assets/3f7564bd-0acb-4e35-9ae9-ee18791cde6a" />

The `-sn` option performs host discovery without performing a port scan.

---

# Port Scanning

<img width="556" height="232" alt="image" src="https://github.com/user-attachments/assets/81d3f728-798f-4a90-bb56-55f600301a0e" />


# Service Detection

<img width="792" height="276" alt="image" src="https://github.com/user-attachments/assets/f1da2562-bf15-4e11-9f70-c3a2c6b79422" />


This attempts to identify:

* Service names
* Software versions

---

# Operating System Detection

Nmap can attempt OS identification:

<img width="737" height="347" alt="image" src="https://github.com/user-attachments/assets/d92027da-c9b1-48e9-b937-c04f1f86e6f1" />

# Scan Results Analysis

The scan provides information about:

* Open ports
* Running services
* Possible attack surfaces

Example:

```
PORT     STATE    SERVICE

135/tcp  open     msrpc
139/tcp  open     netbios
445/tcp  open     smb
```

---

# Security Importance

Port scanning is used by defenders to:

* Audit networks
* Identify unnecessary services
* Reduce attack surface

Attackers may also use scanning during reconnaissance to discover exposed services.

---

# Skills Practiced

* Network reconnaissance
* Port scanning
* Service enumeration
* Firewall configuration
* Security assessment basics
* Understanding exposed services
