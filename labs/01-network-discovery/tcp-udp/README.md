# TCP and UDP (Transport Layer Protocols)

## Objective

The purpose of this section is to understand the role of transport layer protocols and the differences between TCP and UDP communication.

The transport layer is responsible for communication between applications running on different devices.

The two main transport layer protocols are:

* TCP (Transmission Control Protocol)
* UDP (User Datagram Protocol)

---

# TCP vs UDP Comparison

| Feature                | TCP (Transmission Control Protocol)            | UDP (User Datagram Protocol)                 |
| ---------------------- | ---------------------------------------------- | -------------------------------------------- |
| **Type of protocol**   | Connection-oriented protocol                   | Connectionless protocol                      |
| **Connection setup**   | Requires a connection before sending data      | Sends data without establishing a connection |
| **Handshake**          | Uses a three-way handshake (SYN, SYN-ACK, ACK) | No handshake                                 |
| **Reliability**        | Reliable delivery with acknowledgments         | No guarantee of delivery                     |
| **Packet ordering**    | Ensures packets arrive in the correct order    | Packets may arrive out of order              |
| **Error handling**     | Detects errors and retransmits lost packets    | Minimal error checking                       |
| **Speed**              | Slower due to additional controls              | Faster due to lower overhead                 |

---

# Communication Process

<img width="1000" height="470" alt="image" src="https://github.com/user-attachments/assets/01979e45-5611-4e1f-bc4d-beacc9233410" />

---

# Packet Behavior

| TCP                                | UDP                            |
| ---------------------------------- | ------------------------------ |
| Uses TCP flags: SYN, ACK, FIN, RST | No TCP flags                   |
| Uses sequence numbers              | No sequence tracking           |
| Uses acknowledgments               | No acknowledgments             |
| Retransmits lost packets           | Lost packets are not recovered |

---

# Common Uses

| TCP Services     | UDP Services          |
| ---------------- | --------------------- |
| HTTP (Port 80)   | DNS (Port 53)         |
| HTTPS (Port 443) | DHCP (Ports 67/68)    |
| SSH (Port 22)    | SNMP (Port 161)       |
| FTP (Port 21)    | Online gaming         |
| SMB (Port 445)   | Video/audio streaming |

---

# Security Considerations

| TCP Security                 | UDP Security              |
| ---------------------------- | ------------------------- |
| SYN flood attacks            | UDP flood attacks         |
| TCP session hijacking        | DNS amplification attacks |
| Port scanning                | UDP service enumeration   |
| Unauthorized TCP connections | Spoofed UDP traffic       |

---

# Key Takeaways

| TCP                                       | UDP                                                       |
| ----------------------------------------- | --------------------------------------------------------- |
| Best when reliability is important        | Best when speed is important                              |
| Used for web, remote access, file sharing | Used for real-time communication and lightweight services |
| More secure through connection control    | Requires additional security controls at higher layers    |
