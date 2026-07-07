# TCP Analysis Using Wireshark

## Objective

The purpose of this section is to analyze TCP communication using Wireshark and understand the differences between connection-oriented and connectionless protocols.

This lab demonstrates:

* TCP three-way handshake
* TCP flags and connection establishment
* Packet analysis using Wireshark

---

## Lab Environment

| Machine       | Operating System | Role                        |
| ------------- | ---------------- | --------------------------- |
| Kali Linux VM | Linux            | Packet capture and analysis |
| Windows VM    | Windows          | Target machine              |

Both machines were connected to the same internal network.

---

## Tools Used

* Wireshark
* Nmap

---

# 1. TCP scan Analysis

## Open port (445)

<img width="587" height="197" alt="image" src="https://github.com/user-attachments/assets/1cd55e00-8976-4d37-a826-fa32e8b974f7" />

<img width="1342" height="115" alt="image" src="https://github.com/user-attachments/assets/ac03f0b7-717f-4640-bcd4-973f52abfbb0" />

Packets 1–2: Standard ARP resolution again (.10 resolving .20's MAC before sending TCP traffic).
Packet 3: 192.168.56.10 → 192.168.56.20, 35260 → 445 [SYN] — .10 initiates a connection to port 445, sending the first part of the three-way handshake.
Packet 4: 192.168.56.20 → 192.168.56.10, 445 → 35260 [SYN, ACK] — .20 responds confirming port 445 is open and listening. This is the key evidence: an open port replies with SYN,ACK, not RST,ACK.
Packet 5: 192.168.56.10 → 192.168.56.20, 35260 → 445 [ACK] — .10 completes the handshake. At this point, a full TCP connection is established (SYN → SYN,ACK → ACK = classic 3-way handshake).
Packet 6: 192.168.56.10 → 192.168.56.20, 35260 → 445 [RST, ACK] — .10 immediately tears down the connection with a RST. 

## Closed port (23)

<img width="560" height="197" alt="image" src="https://github.com/user-attachments/assets/db0a5b23-522c-4752-8302-9071deaa4f1f" />

<img width="1327" height="97" alt="image" src="https://github.com/user-attachments/assets/e47a702a-49bb-45ea-be97-be23c236eb9f" />
          
Packets 1–2: ARP resolution, .10 learns .20's MAC (same as always, needed before any TCP traffic).
Packet 3: 192.168.56.10 → 192.168.56.20, 42592 → 23 [SYN] — .10 sends a SYN to port 23 (Telnet), attempting to open a connection.
Packet 4: 192.168.56.20 → 192.168.56.10, 23 → 42592 [RST, ACK] — .20 immediately rejects it with RST,ACK. No handshake completes at all. This confirms port 23 is closed.

# 2. TCP SYN scan Analysis

<img width="532" height="197" alt="image" src="https://github.com/user-attachments/assets/315bd857-ea4c-475a-a8b3-16283227652d" />

<img width="1200" height="66" alt="image" src="https://github.com/user-attachments/assets/45471bac-657d-444c-9cd9-3e8add69a913" />

While TCP connect scans complete the full 3-way-handshake, SYN Scans stop halfway and send a RST TCP packet. 
that’s why SYN scans are known as “Half‑open scans” or “Stealth scans”.
Since SYN scans never establish a connection:
➡️**Nothing gets logged** at the application level. This makes SYN scans **quieter for hackers: invisible for old IDs since they only make an alert when they have this session pattern (syn→syn/ack→ack) but not invisible for modern IDs because they scan each packet and *can still detect them through traffic pattern analysis.***  **They flag it as port scanning behavior**.***)***
➡️SYN scans are significantly faster than a standard TCP Connect scan.

# 3. TCP ACK scan Analysis

<img width="562" height="197" alt="image" src="https://github.com/user-attachments/assets/bb6f926c-d020-4a12-a988-1f3ae21eeca8" />

<img width="1297" height="61" alt="image" src="https://github.com/user-attachments/assets/8a1e28b0-7d06-4f92-9b51-21c58971e0f2" />

An ACK scan cannot determine whether a port is open or closed. Its primary purpose is to identify whether ports are filtered or unfiltered by a firewall.
  Unfiltered → The firewall allows the ACK packet to reach the target.
  Filtered → A firewall or packet filter blocked the packet, so Nmap could not determine the port's state.

---

# TCP Scan Comparison

| Scan                 | Command                  | Purpose                                           | How It Works                                                                                          | Typical Result                                                        |
| -------------------- | ------------------------ | ------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| **TCP Connect Scan** | `nmap -sT <target>`      | Identify open TCP ports using a full connection   | Completes the full TCP three-way handshake (SYN → SYN/ACK → ACK) before closing the connection        | `open`, `closed`, or `filtered` ports                                 |
| **TCP SYN Scan**     | `sudo nmap -sS <target>` | Discover open TCP ports using a stealthier method | Sends a SYN packet, waits for a SYN/ACK response, then sends RST instead of completing the connection | `open`, `closed`, or `filtered` ports                                 |
| **TCP ACK Scan**     | `nmap -sA <target>`      | Analyze firewall filtering rules                  | Sends TCP ACK packets to determine whether a firewall is filtering traffic                            | `filtered` or `unfiltered` (does **not** determine if a port is open) |

---

## Skills Learned

* Performed TCP reconnaissance using Nmap.
* Compared TCP Connect, TCP SYN, and TCP ACK scans.
* Identified open, closed, filtered, and unfiltered ports.
* Analyzed TCP packets and flags using Wireshark.
* Understood the TCP three-way handshake.
* Interpreted scan results to assess network exposure and firewall behavior.








