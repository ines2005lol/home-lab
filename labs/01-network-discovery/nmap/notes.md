# Nmap Notes

## Basic Scans

* `-sS` → **TCP SYN scan** (stealth scan, most commonly used)
* `-sT` → **TCP Connect scan** (full TCP 3-way handshake, more visible/logged)
* `-sU` → **UDP scan**
* `-sA` → **TCP ACK scan** (firewall detection)

---

## Port Selection

* `-p 80` → **Scan a specific port**
* `-p 1-1000` → **Scan a port range**
* `-p-` → **Scan all 65535 ports**
* `--top-ports 100` → **Scan the 100 most common ports**

---

## Service & Version Detection

* `-sV` → **Detect service versions**
* `--version-all` → **Aggressive version detection**

---

## OS & Scripts

* `-O` → **Operating System detection**
* `-A` → **Aggressive scan** (OS detection + version detection + scripts + traceroute)
* `--script=default` → **Run default NSE scripts**
* `--script=vuln` → **Run vulnerability detection scripts** ⚠️

---

## Speed & Timing

* `-T0` → **Very slow scan (stealthy)**
* `-T3` → **Normal/default speed**
* `-T4` → **Fast scan (commonly used)**
* `-T5` → **Very fast scan (noisy)**

---

## Output

* `-oN scan.txt` → **Normal output**
* `-oG scan.grep` → **Grepable output**
* `-oX scan.xml` → **XML output**
* `-oA scan` → **Save all output formats**

---

## Host Discovery

* `-sn` → **Ping scan (host discovery only, no port scan)**
* `-Pn` → **Skip ping discovery (assume host is up)**
* `-PS23` → **TCP SYN ping on port 23**
* `-PA21` → **TCP ACK ping on port 21**

---

## Common Recon Examples

```bash
nmap -sn 192.168.56.0/24
```

→ Discover active hosts

```bash
sudo nmap -sS 192.168.56.20
```

→ SYN scan target ports

```bash
nmap -sV 192.168.56.20
```

→ Detect running services and versions

```bash
sudo nmap -A 192.168.56.20
```

→ Full aggressive scan

```bash
nmap -p- 192.168.56.20
```

→ Scan all ports
