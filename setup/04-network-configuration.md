# Internal Network Setup

## Objective

Create an isolated internal network between a Kali Linux virtual machine and a Windows 10 virtual machine to simulate a cybersecurity lab environment.

## Lab Environment

| Machine    | OS         | Role                                | IP Address    |
| ---------- | ---------- | ----------------------------------- | ------------- |
| Kali Linux | Kali Linux | Attacker / Security Testing Machine | 192.168.56.10 |
| Windows 10 | Windows 10 | Target Machine                      | 192.168.56.20 |

## Network Configuration

The virtual machines were connected using a VirtualBox **Internal Network**.

Configuration:

* Network type: Internal Network
* Network name: intnet
* Subnet: 192.168.56.0/24
* Subnet mask: 255.255.255.0
* Internet access: Disabled (fully isolated environment)

This configuration creates a private lab environment where only the connected virtual machines can communicate with each other.

## Windows Firewall Configuration

Windows Firewall blocked incoming ICMP echo requests by default, preventing ping tests from Kali Linux.

To allow network connectivity testing, an inbound firewall rule was enabled:

1. Opened **Windows Defender Firewall with Advanced Security**
2. Navigated to **Inbound Rules**
3. Enabled:

```text
File and Printer Sharing (Echo Request - ICMPv4-In)
```

This allowed ICMP ping requests while keeping Windows Firewall active.

## Connectivity Verification

Connectivity was verified using ICMP ping.

From Kali Linux:

```bash
ping 192.168.56.20
```

From Windows Command Prompt:

```cmd
ping 192.168.56.10
```

Successful replies confirmed communication between both machines.
