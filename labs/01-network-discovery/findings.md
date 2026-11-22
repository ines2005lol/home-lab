# Lab 01 – Findings Report

A short assessment-style summary of what Lab 01 found, written the way findings are reported in a real security assessment: scope, method, results, risk and recommendations.

## 1. Scope

| Item | Value |
| ---- | ----- |
| Target | Windows 10 VM – `192.168.56.20` |
| Tester machine | Kali Linux VM – `192.168.56.10` |
| Network | VirtualBox Internal Network `intnet`, `192.168.56.0/24`, no internet access |
| Authorisation | Both machines are owned by me; testing was limited to this isolated lab |
| Out of scope | The host machine, the home network, any external system |

## 2. Methodology

1. **Connectivity check** – ICMP ping in both directions ([icmp.md](arp-icmp/icmp.md)).
2. **Layer 2 discovery** – inspected ARP tables and captured ARP resolution in Wireshark ([arp.md](arp-icmp/arp.md), [wireshark.md](arp-icmp/wireshark.md)).
3. **Host discovery** – `nmap -sn` ping scan of the subnet ([nmap.md](nmap-intro/nmap.md)).
4. **TCP port scanning** – Connect (`-sT`), SYN (`-sS`) and ACK (`-sA`) scans, each verified packet by packet in Wireshark ([tcp-wireshark.md](tcp-udp/tcp-wireshark.md)).
5. **Service and OS detection** – `nmap -sV` and `nmap -O` ([nmap.md](nmap-intro/nmap.md)).
6. **UDP scanning** – `nmap -sU` against a Netcat UDP listener ([udp-wireshark.md](tcp-udp/udp-wireshark.md)).

## 3. Summary of Findings

Severity reflects the risk **if the same configuration existed on a real network**, not inside this isolated lab.

| ID | Finding | Severity |
| -- | ------- | -------- |
| F1 | Target runs Windows 10, which reached end of support on 14 October 2025 | High |
| F2 | SMB (445/tcp) exposed to the local network | Medium |
| F3 | MS-RPC (135/tcp) and NetBIOS session service (139/tcp) exposed | Low |
| F4 | Hosts on the same subnet can be discovered via ARP regardless of firewall | Informational |
| F5 | ICMP echo allowed through the firewall (enabled intentionally for testing) | Informational |
| F6 | Netcat traffic is sent in plaintext and readable in a packet capture | Informational |

## 4. Detailed Findings

### F1 – Unsupported operating system (High)

**Observation:** The target is a Windows 10 machine. Microsoft ended support for Windows 10 on 14 October 2025; security updates now continue only for devices enrolled in the paid Extended Security Updates (ESU) programme.

**Risk:** Newly discovered vulnerabilities are no longer patched for systems without extended support, so an attacker who finds the exposed services in F2 and F3 has a growing list of unpatched issues to try.

**Recommendation:** In a real environment, upgrade to a supported Windows version or enrol in Extended Security Updates. In this lab, an unpatched target is acceptable and even useful for practice, because the network is isolated.

### F2 – SMB exposed on 445/tcp (Medium)

**Observation:** Port scanning showed `445/tcp open (microsoft-ds)`. The TCP Connect scan capture confirms it: the target answered the SYN with `SYN, ACK`. Together with 135/tcp and 139/tcp (F3), this was one of only three open TCP ports found on the target.

**Risk:** SMB is used for file and printer sharing and is a frequent attack target: brute-forcing credentials, abusing anonymous or guest shares, and historically wormable vulnerabilities such as EternalBlue (MS17-010, exploited by WannaCry) on unpatched systems with SMBv1.

**Recommendation:**

* Block 445/tcp with Windows Defender Firewall for any network that does not need file sharing.
* Make sure SMBv1 is disabled and the system is fully patched.
* Disable guest access and use strong passwords for accounts that can authenticate over SMB.

### F3 – MS-RPC and NetBIOS exposed on 135/tcp and 139/tcp (Low)

**Observation:** Port scanning showed `135/tcp open (msrpc)` and `139/tcp open (netbios-ssn)`.

**Risk:** These services can leak information about the host (names, users, shares) to an attacker doing enumeration, and they increase the attack surface.

**Recommendation:** Restrict both ports with firewall rules where they are not needed, and disable NetBIOS over TCP/IP in the network adapter settings if no legacy systems depend on it.

### F4 – ARP-based host discovery (Informational)

**Observation:** The Wireshark capture shows the target replying to the ARP request `Who has 192.168.56.20?` with its MAC address `08:00:27:ca:0a:04`. ARP happens below the IP layer, so Windows Firewall cannot hide the host from a machine on the same subnet.

**Risk:** Any device on the same local network can find live hosts, even when ICMP is blocked. ARP also has no authentication, which makes ARP spoofing and man-in-the-middle attacks possible.

**Recommendation:** Segment networks so untrusted devices do not share a subnet with important hosts, and use switch features such as Dynamic ARP Inspection on real networks.

### F5 – ICMP echo allowed (Informational)

**Observation:** Windows Firewall blocks ICMP echo requests by default. For this lab I enabled the built-in rule `File and Printer Sharing (Echo Request - ICMPv4-In)` so connectivity could be tested with ping.

**Risk:** Hosts that answer ping are easy to find with a ping sweep. This is low risk on its own, but it makes reconnaissance faster.

**Recommendation:** Keep the rule only where ICMP is needed for troubleshooting. The firewall itself stayed enabled, which is the right approach compared with turning the whole firewall off.

### F6 – Plaintext traffic with Netcat (Informational)

**Observation:** Data sent from Kali to the Netcat UDP listener on 9999/udp was fully readable in Wireshark.

**Risk:** Any tool or protocol without encryption exposes its contents to anyone who can capture traffic on the network path.

**Recommendation:** Use encrypted alternatives (for example `ncat --ssl`, SSH or TLS-based services) when transferring anything sensitive.

## 5. Testing Notes

* For the full port and service scans, Windows Firewall was temporarily disabled so ports would show as `open` or `closed` instead of `filtered`. It was re-enabled afterwards. A better approach for future labs is to allow only the specific ports being tested.
* Port 23/tcp (Telnet) was confirmed **closed**: the target answered the SYN with `RST, ACK`.
* The ACK scan only shows whether a firewall filters traffic (`filtered` / `unfiltered`); it cannot tell whether a port is open.
* UDP port 9999 with an active Netcat listener was reported as `open|filtered`, because UDP services often send no reply.

## 6. Lessons Learned

* Scan results only mean something when you understand the packets behind them: `SYN/ACK` means open, `RST/ACK` means closed, and no answer usually means filtered.
* A host firewall changes scan results dramatically, so always record the firewall state when you report findings.
* UDP scanning is slower and less certain than TCP scanning because of the lack of responses.
* Writing findings with risk and remediation, not just tool output, is what turns a scan into a useful assessment.
