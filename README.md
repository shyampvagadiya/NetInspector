# NetInspector

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.x-blue?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Platform-CLI-lightgrey?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Version-1.0.1-green?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge"/>
</p>

> **Scan. Analyze. Protect.**

NetInspector is a Python-based, CLI-only network reconnaissance and traffic analysis tool combining a port scanner and a live packet sniffer/analyzer in a single utility. Designed for security practitioners, network administrators, and students who need a lightweight, terminal-friendly tool that works even on headless servers.

---

## Features

### 🔍 ICMP Scan (Ping Sweep)
- Probe the availability of one or multiple hosts simultaneously
- Input comma-separated IPs for batch scanning
- Reports each host as **UP** or **DOWN** with elapsed scan time
- Gracefully flags invalid address formats

### 🔌 Port Scanner
- Supports **TCP** and **UDP** scanning modes
- **Single host scan** — target a specific IP and a set of comma-separated ports
- **Range scan** — iterate over a subnet range (e.g. `192.168.1.1` to `192.168.1.50`) and scan specified ports across all hosts
- Performs reverse DNS resolution to display hostnames alongside IPs
- Identifies service names for open ports via `socket.getservbyport`
- Reports port status as `OPEN` or `Closed|Filtered`

### 📡 Packet Analyzer / Sniffer
- **Live capture** on any network interface detected on the host
- Auto-enables monitor mode when a Wi-Fi interface is selected
- BPF filter support — filter by protocol (TCP/UDP/ICMP) and optionally by port
- Toggle between **summarized** and **full packet detail** output
- Export captured traffic to timestamped `.pcap` files for offline analysis
- **Open existing `.cap`/`.pcap` files** — load and inspect previously captured traffic using Scapy, with summary or per-packet detail view

---

## Tech Stack & Libraries

| Library | Role |
|---|---|
| `scapy` | Packet crafting, pcap file reading, packet dissection |
| `pyshark` | Live packet capture via TShark/Wireshark backend |
| `icmplib` | ICMP ping operations and host availability checks |
| `psutil` | Network interface enumeration |
| `socket` | TCP/UDP port scanning, hostname resolution, service identification |
| `pyfiglet` | ASCII art banner rendering |
| `termcolor` / `colorama` | Terminal color output |

---

## Installation

**Prerequisites:** Python 3.x, TShark (required by pyshark for live capture)

```bash
# Clone the repository
git clone https://github.com/shyampvagadiya/NetInspector.git
cd NetInspector

# Install dependencies
pip install -r requirements.txt

# Run the tool (requires elevated privileges for packet capture)
sudo python3 netinspecor.py
```

> **Note:** Root/Administrator privileges are required for live packet capture and raw socket operations.

---

## Usage

On launch, NetInspector displays an interactive CLI menu:

```
  ___  ___  ___  ___  ___  ___
  NetInspector  —  Scan . Analyze . Protect.

  Choose the Operation:

    1. ICMP Scan
    2. Port Scan
    3. Packet Sniffing/Analyzer
    Q. Quit
```

### ICMP Scan
```
Enter IPs separated by comma: 192.168.1.1,192.168.1.2,8.8.8.8
192.168.1.1  is  UP.
192.168.1.2  is  DOWN.
8.8.8.8      is  UP.
Scan completed in  0:00:03.142  Seconds.
```

### Port Scan
```
Select Scan Type: [TCP/UDP/ICMP]: TCP
1. Scan Single host
2. Scan a range of hosts

Target Host: 192.168.1.1
Ports (comma ',' separated): 22,80,443,8080

PORT    STATUS          SERVICE
22      OPEN            ssh
80      OPEN            http
443     OPEN            https
8080    Closed|Filtered
```

### Packet Analyzer
```
1. Start new packet capture
2. Open Existing .cap/.pcap file
3. Go to main menu

Select Interface: Wi-Fi
Summarized capture? [y/N]: y
Filter packets? [y/N]: y
Type [TCP/UDP/ICMP]: TCP
Specific Protocol (Port): 443
```

---

## Project Structure

```
NetInspector/
├── netinspecor.py      # Main application — all core logic
├── requirements.txt    # Python dependencies
└── setup.py            # Package setup configuration
```

---

## Requirements

See `requirements.txt` for the full dependency list. Key packages:

```
scapy
pyshark
icmplib
psutil
pyfiglet
termcolor
colorama
```

---

## Disclaimer

This tool is intended strictly for **authorized testing, educational purposes, and legitimate network administration** on networks you own or have explicit permission to test. Unauthorized scanning or packet capture may violate local laws and regulations. The developer assumes no liability for misuse.

---

## Author

**Shyam Vagadiya**  
Cybercrime & Threat Intelligence Analyst

[![GitHub](https://img.shields.io/badge/GitHub-shyampvagadiya-black?style=flat&logo=github)](https://github.com/shyampvagadiya/NetInspector)

---

*NetInspector v1.0.1 — CLI-based network scanning and packet analysis utility*
