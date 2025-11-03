# NMAP - Network Mapper
## Complete Network Scanning Tool Repository

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/Version-1.0-blue.svg)](https://github.com/)
[![Nmap Version](https://img.shields.io/badge/Nmap-7.94+-green.svg)](https://nmap.org/)

> A comprehensive guide and toolkit for using Nmap, the industry-standard network scanning and security auditing tool. This repository contains installation instructions, configurations, usage examples, practical scripts, and live demonstrations.

---

## 📋 Table of Contents

- [About Nmap](#about-nmap)
- [Features](#features)
- [Installation](#installation)
  - [Linux](#linux-installation)
  - [Windows](#windows-installation)
  - [macOS](#macos-installation)
- [Quick Start](#quick-start)
- [Usage Examples](#usage-examples)
  - [Basic Scanning](#basic-scanning)
  - [Advanced Scanning](#advanced-scanning)
  - [Vulnerability Detection](#vulnerability-detection)
- [Configuration](#configuration)
- [Scripts and Tools](#scripts-and-tools)
- [Live Demos](#live-demos)
- [Troubleshooting](#troubleshooting)
- [Best Practices](#best-practices)
- [Contributing](#contributing)
- [License](#license)

---

## 🔍 About Nmap

**Nmap** (Network Mapper) is a powerful, open-source network scanning tool created by Gordon Lyon in September 1997. It is used for network discovery, security auditing, vulnerability assessment, and network mapping.

With millions of downloads and approximately 400,000 registered users, Nmap has become the industry standard for network reconnaissance and is widely trusted by security professionals, penetration testers, and network administrators worldwide.

### Why Use Nmap?

- **Network Discovery**: Quickly identify all devices connected to a network
- **Port Scanning**: Determine which ports are open and which services are running
- **Service Detection**: Identify running applications and their versions
- **OS Fingerprinting**: Determine the operating system and version of target devices
- **Vulnerability Assessment**: Identify potential vulnerabilities through NSE scripts
- **Security Auditing**: Conduct comprehensive security assessments
- **Network Inventory**: Maintain accurate records of network devices and services
- **Incident Response**: Quickly assess the network during security incidents

### Key Features

- Host Discovery using various ping methods
- Port Scanning with multiple techniques (TCP SYN, TCP Connect, UDP, etc.)
- Service and Version Detection
- Operating System Detection
- NSE (Nmap Scripting Engine) for advanced scanning
- Multiple Output Formats (Normal, XML, Grepable, Script Kiddie)
- Zenmap GUI for visual interaction
- Stealth Options and Firewall Evasion Techniques

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| **Real-Time Analysis** | Monitor network traffic and detect threats as they occur |
| **Protocol Analysis** | Understand and analyze various network protocols (TCP, UDP, ICMP, etc.) |
| **Content Matching** | Identify malicious patterns in network traffic |
| **Attack Detection** | Detect buffer overflows, port scans, DoS attacks, SQL injection, and more |
| **Flexible Rules** | Customize detection through user-defined configurations |
| **Multiple Modes** | Function as sniffer, packet logger, or full NIDS/IPS |
| **Cross-Platform** | Works on Linux, Windows, Unix, and BSD systems |
| **Open Source** | Free, community-driven, with active development |

---

## 📦 Installation

### Linux Installation

#### Ubuntu/Debian

```bash
# Update package lists
sudo apt update

# Install Nmap
sudo apt install nmap -y

# Verify installation
nmap -V
```

#### Red Hat/CentOS/Fedora

```bash
# Install Nmap
sudo yum install nmap -y

# Or using dnf (newer systems)
sudo dnf install nmap -y

# Verify installation
nmap -V
```

#### Arch Linux

```bash
# Install Nmap
sudo pacman -S nmap

# Verify installation
nmap -V
```

### Windows Installation

1. **Download Installer**
   - Visit [nmap.org/download](https://nmap.org/download)
   - Download latest `.exe` installer
   - Look for "Microsoft Windows binaries" section

2. **Install Npcap** (Required for packet capture)
   - Download from [npcap.com](https://npcap.com)
   - Install in WinPcap API-compatible mode
   - Required for Nmap to capture packets

3. **Install Visual C++ Redistributable**
   - Download from Microsoft website
   - Install Visual C++ Redistributable 2015-2019 (x64)

4. **Run Installer**
   - Double-click `nmap-setup.exe`
   - Follow installation wizard
   - Default location: `C:\Program Files (x86)\Nmap`

5. **Verify Installation**
   ```cmd
   nmap -V
   ```

### macOS Installation

#### Using Homebrew (Recommended)

```bash
# Install Homebrew (if not installed)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install Nmap
brew install nmap

# Verify installation
nmap -V
```

#### Using DMG Installer

1. Download `.dmg` file from [nmap.org](https://nmap.org/download)
2. Double-click to mount
3. Run installer package
4. Follow installation prompts
5. Verify: `nmap -V`

---

## 🚀 Quick Start

### Basic Network Scan

```bash
# Discover all active hosts on your network
sudo nmap -sn 192.168.1.0/24

# Scan a single target
sudo nmap 192.168.1.1

# Scan with service version detection
sudo nmap -sV 192.168.1.1

# Full aggressive scan
sudo nmap -A 192.168.1.1
```

### Check if Nmap is Working

```bash
# Display version
nmap -V

# Get help
nmap -h

# Run self-test (scans localhost)
nmap localhost
```

---

## 📖 Usage Examples

### Basic Scanning

#### Discover Active Hosts

```bash
# Ping scan (host discovery only)
sudo nmap -sn 192.168.1.0/24
```

**Output:**
```
Nmap scan report for 192.168.1.1
Host is up (0.0012s latency).
Nmap scan report for 192.168.1.50
Host is up (0.0045s latency).
```

#### Basic Port Scan

```bash
# SYN scan (default, requires root)
sudo nmap -sS 192.168.1.1

# TCP Connect scan (no root required)
nmap -sT 192.168.1.1
```

#### Scan Specific Ports

```bash
# Single port
nmap -p 80 192.168.1.1

# Multiple ports
nmap -p 22,80,443,3306 192.168.1.1

# Port range
nmap -p 1-1000 192.168.1.1

# All ports
nmap -p- 192.168.1.1

# Top 100 ports (fast)
nmap -F 192.168.1.1
```

### Advanced Scanning

#### Service Version Detection

```bash
# Identify running service versions
sudo nmap -sV 192.168.1.1
```

**Output:**
```
PORT     STATE SERVICE     VERSION
22/tcp   open  ssh         OpenSSH 7.4
80/tcp   open  http        Apache httpd 2.4.6
3306/tcp open  mysql       MySQL 5.7.31
```

#### Operating System Detection

```bash
# Detect OS (requires root)
sudo nmap -O 192.168.1.1

# Guess OS if confidence is low
sudo nmap -O --osscan-guess 192.168.1.1
```

#### Aggressive Scan

```bash
# Full aggressive scan with everything
sudo nmap -A -T4 192.168.1.1

# Components:
# -A: Aggressive (OS detection, service detection, script scanning, traceroute)
# -T4: Aggressive timing (faster)
```

#### Scan from File

```bash
# Create targets.txt with one IP per line
echo "192.168.1.1" > targets.txt
echo "192.168.1.50" >> targets.txt

# Scan all targets in file
sudo nmap -iL targets.txt
```

### Vulnerability Detection

#### Default NSE Scripts

```bash
# Run default security checks
sudo nmap -sC 192.168.1.1
```

#### Vulnerability Scanning

```bash
# Run vulnerability detection scripts
sudo nmap --script vuln 192.168.1.1

# Check specific vulnerabilities
sudo nmap --script smb-vuln* -p 445 192.168.1.1

# Check SSL/TLS issues
sudo nmap --script ssl-enum-ciphers -p 443 192.168.1.1
```

#### Full Vulnerability Audit

```bash
# Comprehensive vulnerability scan
sudo nmap -sV --script vuln,default -p- 192.168.1.1 -oX results.xml
```

---

## 🔧 Configuration

### Common Command Options

| Option | Description | Example |
|--------|-------------|---------|
| `-sn` | Ping scan only (host discovery) | `nmap -sn 192.168.1.0/24` |
| `-sS` | TCP SYN scan (default) | `sudo nmap -sS 192.168.1.1` |
| `-sT` | TCP Connect scan | `nmap -sT 192.168.1.1` |
| `-sU` | UDP scan | `sudo nmap -sU 192.168.1.1` |
| `-sV` | Service version detection | `sudo nmap -sV 192.168.1.1` |
| `-O` | OS detection | `sudo nmap -O 192.168.1.1` |
| `-A` | Aggressive scan | `sudo nmap -A 192.168.1.1` |
| `-sC` | Default NSE scripts | `sudo nmap -sC 192.168.1.1` |
| `-p` | Specify ports | `nmap -p 80,443,3306 192.168.1.1` |
| `-Pn` | Skip ping (assume host up) | `nmap -Pn 192.168.1.1` |
| `-T` | Timing template (0-5) | `nmap -T4 192.168.1.1` |
| `-oN` | Normal output | `nmap 192.168.1.1 -oN results.txt` |
| `-oX` | XML output | `nmap 192.168.1.1 -oX results.xml` |
| `-oA` | All output formats | `nmap 192.168.1.1 -oA results` |

### Timing Templates

```bash
# Paranoid (very slow, stealth)
nmap -T0 192.168.1.1

# Sneaky (slow, stealth)
nmap -T1 192.168.1.1

# Polite (slower, less bandwidth)
nmap -T2 192.168.1.1

# Normal (default, balanced)
nmap -T3 192.168.1.1

# Aggressive (fast)
nmap -T4 192.168.1.1

# Insane (very fast, may miss)
nmap -T5 192.168.1.1
```

### Output Options

```bash
# Save to file (human-readable)
nmap 192.168.1.1 -oN results.txt

# Save to XML (machine-readable)
nmap 192.168.1.1 -oX results.xml

# Save to Grepable format
nmap 192.168.1.1 -oG results.grep

# Save in all formats
nmap 192.168.1.1 -oA results

# Verbose output
nmap -v 192.168.1.1

# Very verbose
nmap -vv 192.168.1.1
```

---

## 🛠️ Scripts and Tools

### Bash Script: Quick Scan

Create `quick-scan.sh`:

```bash
#!/bin/bash

# Quick Network Scan Script
# Usage: ./quick-scan.sh 192.168.1.1

if [ -z "$1" ]; then
    echo "Usage: $0 <target_ip>"
    exit 1
fi

TARGET=$1
TIMESTAMP=$(date +%Y%m%d_%H%M%S)
OUTPUT_DIR="scan_results_$TIMESTAMP"

mkdir -p "$OUTPUT_DIR"

echo "Starting quick scan of $TARGET..."
echo "Results will be saved to $OUTPUT_DIR"

# Run scans
echo "[*] Running host discovery..."
sudo nmap -sn $TARGET -oN "$OUTPUT_DIR/01_host_discovery.txt"

echo "[*] Running port scan..."
sudo nmap -sS -T4 $TARGET -oN "$OUTPUT_DIR/02_port_scan.txt"

echo "[*] Running service detection..."
sudo nmap -sV $TARGET -oN "$OUTPUT_DIR/03_service_detection.txt"

echo "[*] Running vulnerability scan..."
sudo nmap --script vuln $TARGET -oN "$OUTPUT_DIR/04_vulnerabilities.txt"

echo "[*] Running aggressive scan..."
sudo nmap -A -T4 $TARGET -oA "$OUTPUT_DIR/05_aggressive_scan"

echo "[✓] Scan complete! Results saved to $OUTPUT_DIR"
```

**Usage:**
```bash
chmod +x quick-scan.sh
./quick-scan.sh 192.168.1.1
```

### Bash Script: Subnet Scan

Create `subnet-scan.sh`:

```bash
#!/bin/bash

# Subnet Scan Script
# Usage: ./subnet-scan.sh 192.168.1.0/24

if [ -z "$1" ]; then
    echo "Usage: $0 <network_cidr>"
    exit 1
fi

NETWORK=$1

echo "Scanning network: $NETWORK"

# Discover active hosts
echo "[*] Discovering active hosts..."
sudo nmap -sn $NETWORK -oG host_discovery.grep

# Extract IPs from grepable output
echo "[*] Extracting active IPs..."
grep "Host" host_discovery.grep | cut -d' ' -f2 > active_hosts.txt

echo "[*] Found $(wc -l < active_hosts.txt) active hosts"

# Scan each host
echo "[*] Scanning each host for open ports..."
sudo nmap -sS -T4 -iL active_hosts.txt -oN network_scan.txt

echo "[✓] Scan complete!"
echo "Results:"
echo "  - Active hosts: active_hosts.txt"
echo "  - Host discovery: host_discovery.grep"
echo "  - Network scan: network_scan.txt"
```

**Usage:**
```bash
chmod +x subnet-scan.sh
./subnet-scan.sh 192.168.1.0/24
```

### Bash Script: Vulnerability Assessment

Create `vuln-assessment.sh`:

```bash
#!/bin/bash

# Vulnerability Assessment Script
# Usage: ./vuln-assessment.sh 192.168.1.1

if [ -z "$1" ]; then
    echo "Usage: $0 <target_ip>"
    exit 1
fi

TARGET=$1
TIMESTAMP=$(date +%Y%m%d_%H%M%S)
OUTPUT="vulnerability_assessment_$TARGET_$TIMESTAMP.txt"

echo "Starting vulnerability assessment of $TARGET"
echo "Output: $OUTPUT"

{
    echo "╔════════════════════════════════════════════════════════════╗"
    echo "║        NMAP VULNERABILITY ASSESSMENT REPORT                ║"
    echo "╚════════════════════════════════════════════════════════════╝"
    echo ""
    echo "Target: $TARGET"
    echo "Timestamp: $(date)"
    echo ""
    echo "─────────────────────────────────────────────────────────────"
    echo "1. SERVICE DETECTION"
    echo "─────────────────────────────────────────────────────────────"
    sudo nmap -sV $TARGET
    
    echo ""
    echo "─────────────────────────────────────────────────────────────"
    echo "2. VULNERABILITY SCAN"
    echo "─────────────────────────────────────────────────────────────"
    sudo nmap --script vuln $TARGET
    
    echo ""
    echo "─────────────────────────────────────────────────────────────"
    echo "3. OS DETECTION"
    echo "─────────────────────────────────────────────────────────────"
    sudo nmap -O $TARGET
    
} | tee "$OUTPUT"

echo "[✓] Assessment complete! Report saved: $OUTPUT"
```

**Usage:**
```bash
chmod +x vuln-assessment.sh
./vuln-assessment.sh 192.168.1.1
```

---

## 🎯 Live Demos

### Demo 1: Basic Network Reconnaissance

```bash
# Step 1: Discover active hosts
sudo nmap -sn 192.168.1.0/24

# Step 2: Basic port scan
sudo nmap -sS 192.168.1.50

# Step 3: Service detection
sudo nmap -sV 192.168.1.50

# Step 4: Comprehensive scan
sudo nmap -A 192.168.1.50 -oA demo1_results
```

### Demo 2: Vulnerability Detection

```bash
# Step 1: Default NSE scripts
sudo nmap -sC 192.168.1.50

# Step 2: Vulnerability scan
sudo nmap --script vuln 192.168.1.50

# Step 3: Specific vulnerability checks
sudo nmap --script smb-vuln* -p 445 192.168.1.50

# Step 4: Complete vulnerability report
sudo nmap -sV --script vuln,default -p- 192.168.1.50 -oX demo2.xml
```

### Demo 3: Comprehensive Security Audit

```bash
# Step 1: Aggressive scan with all detection methods
sudo nmap -A -T4 -sV -sC -O --script vuln -p- 192.168.1.50 -oA demo3_audit

# Step 2: Compare multiple targets
sudo nmap -A -T4 192.168.1.1 192.168.1.50 192.168.1.100 -oA network_audit

# Step 3: Network traceroute
sudo nmap --traceroute 192.168.1.50

# Step 4: Full network scan
sudo nmap -A -T4 192.168.1.0/24 -oA complete_network_audit
```

---

## 🔧 Troubleshooting

### Common Issues and Solutions

| Issue | Solution |
|-------|----------|
| **Host seems down** | Use `-Pn` flag: `nmap -Pn 192.168.1.1` |
| **Permission denied** | Use `sudo`: `sudo nmap -sS 192.168.1.1` |
| **Timeout errors** | Increase timeout: `nmap -T4 192.168.1.1` |
| **No open ports found** | Scan all ports: `nmap -p- 192.168.1.1` |
| **Service detection failed** | Increase intensity: `nmap -sV --version-intensity 9 192.168.1.1` |
| **Firewall blocking** | Try different scan: `nmap -sT 192.168.1.1` |
| **RST from your IP** | Check firewall: Disable local firewall or use `-sT` |

### Testing Installation

```bash
# Test scan on localhost
nmap localhost

# Test connectivity
ping -c 4 192.168.1.1

# Test specific port
nmap -p 80 192.168.1.1
```

---

## 📋 Best Practices

### Before Scanning

1. **Get Authorization**
   - Obtain written permission before scanning any network
   - Specify scope and timeframe
   - Keep authorization documentation

2. **Plan Your Scans**
   - Identify targets beforehand
   - Scan during off-peak hours if possible
   - Document scanning procedures

### During Scanning

1. **Use Appropriate Timing**
   - Use `-T3` for normal operations
   - Use `-T1` or `-T2` for stealth (if authorized)
   - Avoid `-T5` on production networks

2. **Minimize Impact**
   - Use `-F` for quick assessment
   - Scan fewer ports initially
   - Increase scope gradually

3. **Keep Records**
   - Always save results: `-oA results`
   - Document findings
   - Note any unusual responses

### After Scanning

1. **Verify Findings**
   - Manually verify critical findings
   - Cross-reference with official databases
   - Check for false positives

2. **Maintain Confidentiality**
   - Securely store scan results
   - Share only with authorized personnel
   - Delete unnecessary files

3. **Follow Up**
   - Address identified vulnerabilities
   - Rescan after patches
   - Track remediation progress

---

## 📊 Command Reference

### Essential Commands

```bash
# Network Discovery
nmap -sn 192.168.1.0/24                    # Ping scan
nmap -PS -p 22,80 192.168.1.1              # TCP SYN ping

# Port Scanning
nmap -sS 192.168.1.1                       # TCP SYN (default)
nmap -sT 192.168.1.1                       # TCP Connect
nmap -sU 192.168.1.1                       # UDP scan
nmap -sA 192.168.1.1                       # ACK (firewall mapping)

# Service Detection
nmap -sV 192.168.1.1                       # Service versions
nmap -O 192.168.1.1                        # OS detection
nmap -A 192.168.1.1                        # Aggressive (all)

# Vulnerability Scanning
nmap -sC 192.168.1.1                       # Default NSE scripts
nmap --script vuln 192.168.1.1             # Vulnerability scripts
nmap --script smb-vuln* -p 445 192.168.1.1 # SMB vulnerabilities

# Output Options
nmap 192.168.1.1 -oN results.txt           # Normal format
nmap 192.168.1.1 -oX results.xml           # XML format
nmap 192.168.1.1 -oG results.grep          # Grepable format
nmap 192.168.1.1 -oA results               # All formats
```

---

## 📚 Port Reference

### Common Ports and Services

| Port | Service | Protocol |
|------|---------|----------|
| 21 | FTP | TCP |
| 22 | SSH | TCP |
| 23 | Telnet | TCP |
| 25 | SMTP | TCP |
| 53 | DNS | TCP/UDP |
| 80 | HTTP | TCP |
| 110 | POP3 | TCP |
| 143 | IMAP | TCP |
| 443 | HTTPS | TCP |
| 3306 | MySQL | TCP |
| 3389 | RDP | TCP |
| 5432 | PostgreSQL | TCP |
| 5900 | VNC | TCP |
| 8080 | HTTP Alt | TCP |

---

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📖 Additional Resources

### Official Documentation
- [Nmap Official Website](https://nmap.org/)
- [Nmap Manual](https://nmap.org/book/man.html)
- [Nmap Documentation](https://nmap.org/docs/)

### NSE Scripts
- [NSE Script Database](https://nmap.org/nsedoc/)
- [NSE Script Examples](https://nmap.org/nsedoc/scripts/)

### Learning Resources
- [HackTheBox](https://www.hackthebox.com/) - CTF challenges
- [TryHackMe](https://www.tryhackme.com/) - Interactive labs
- [Nmap Tutorial](https://nmap.org/book/intro.html) - Official tutorial

### Related Tools
- **Zenmap** - GUI for Nmap
- **Wireshark** - Packet analyzer
- **Metasploit** - Exploitation framework
- **Burp Suite** - Web security testing

---

## ⚖️ Legal and Ethical Guidelines

**IMPORTANT:** 

⚠️ **Unauthorized network scanning is illegal in most jurisdictions.**

Before using Nmap:
- ✅ **Always get written authorization** from network owners
- ✅ **Specify scope and timeframe** in authorization
- ✅ **Scan only authorized targets**
- ✅ **Maintain confidentiality** of results
- ✅ **Follow local laws** regarding network testing

Unauthorized scanning may result in:
- Criminal charges
- Civil liability
- Termination of employment
- Fines and imprisonment

---

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

Nmap itself is licensed under its custom license (free for use and redistribution).

---

## 👨‍💻 Author

**Harsh Dhakate**  
MTech Cybersecurity Student  
MIT

---

## 📞 Support

For issues, questions, or suggestions:

1. Check the [Troubleshooting](#troubleshooting) section
2. Visit [Nmap Official Documentation](https://nmap.org/)
3. Open an issue in this repository
4. Contact the community on Nmap mailing lists

---

## 🎓 Acknowledgments

- Gordon Lyon (Fyodor Vaskovich) - Creator of Nmap
- Cisco/Sourcefire - Maintainers of Nmap
- The security community - For continuous feedback and improvements

---

## 📊 Statistics

- **Created**: November 2025
- **Version**: 1.0
- **Nmap Compatibility**: 7.94+
- **Platforms**: Linux, Windows, macOS
- **Commands**: 50+ documented
- **Scripts**: 3+ included
- **Use Cases**: 6+ documented

---

**Happy Scanning!** 🎯

Remember: Use Nmap responsibly and always with proper authorization.

For more information, visit [https://nmap.org](https://nmap.org)
