# Network Scanning

## nmap

### Basic Scans
```bash
# Basic TCP SYN scan
nmap -sS <target>

# Basic TCP connect scan
nmap -sT <target>

# UDP scan
nmap -sU <target>

# Ping scan (host discovery)
nmap -sn <target>

# Skip host discovery
nmap -Pn <target>
```

### Port Scanning
```bash
# Scan specific ports
nmap -p 22,80,443 <target>

# Scan port range
nmap -p 1-1000 <target>

# Scan all 65535 ports
nmap -p- <target>

# Top 1000 ports (default)
nmap --top-ports 1000 <target>

# Fast scan (top 100 ports)
nmap -F <target>
```

### Service Detection
```bash
# Service version detection
nmap -sV <target>

# OS detection
nmap -O <target>

# Aggressive scan (OS, version, scripts, traceroute)
nmap -A <target>

# Default scripts
nmap -sC <target>

# Specific script
nmap --script <script-name> <target>
```

### Timing and Performance
```bash
# Timing templates (0-5, paranoid to insane)
nmap -T4 <target>

# Custom timing
nmap --min-rate 1000 <target>
nmap --max-rate 5000 <target>

# Parallel scanning
nmap --min-parallelism 10 <target>
```

### Output Options
```bash
# Normal output
nmap -oN scan.txt <target>

# XML output
nmap -oX scan.xml <target>

# Grepable output
nmap -oG scan.grep <target>

# All formats
nmap -oA scan <target>
```

### Stealth and Evasion
```bash
# Decoy scan
nmap -D RND:10 <target>

# Source port spoofing
nmap --source-port 53 <target>

# Fragment packets
nmap -f <target>

# Idle zombie scan
nmap -sI <zombie-ip> <target>
```

### NSE Scripts
```bash
# Vulnerability scanning
nmap --script vuln <target>

# SMB enumeration
nmap --script smb-enum-* <target>

# HTTP enumeration
nmap --script http-enum <target>

# SSL/TLS testing
nmap --script ssl-enum-ciphers <target>

# DNS enumeration
nmap --script dns-brute <target>
```

### Common One-Liners
```bash
# Quick TCP scan
nmap -sS -T4 -p- <target>

# Comprehensive scan
nmap -sS -sV -O -A -T4 -p- <target>

# UDP top ports
nmap -sU --top-ports 1000 <target>

# Web service discovery
nmap -p 80,443,8080,8443 --script http-title,http-server-header <target>
```

## masscan

### Basic Usage
```bash
# Basic port scan
masscan -p 80,443 <target>

# Scan port range
masscan -p 1-1000 <target>

# Scan all ports
masscan -p 1-65535 <target>

# Rate limiting
masscan -p 80,443 --rate 1000 <target>
```

### Advanced Options
```bash
# Banner grabbing
masscan -p 80,443 --banners <target>

# Output to file
masscan -p 80,443 -oG output.txt <target>

# Exclude ports
masscan -p 1-1000 --exclude-ports 22,23 <target>

# Random source IP
masscan -p 80,443 --randomize-hosts <target>
```

### Performance Tuning
```bash
# Maximum rate
masscan -p 1-65535 --rate 10000 <target>

# Connection timeout
masscan -p 80,443 --connection-timeout 10 <target>

# Retries
masscan -p 80,443 --retries 3 <target>
```

### Network Ranges
```bash
# CIDR notation
masscan -p 80,443 10.0.0.0/24

# Range notation
masscan -p 80,443 10.0.0.1-10.0.0.254

# Multiple targets
masscan -p 80,443 10.0.0.1 192.168.1.1
```

### Common One-Liners
```bash
# Fast web port scan
masscan -p 80,443,8080,8443 --rate 1000 <target>

# All ports fast
masscan -p 1-65535 --rate 10000 <target>

# Top ports with banners
masscan --top-ports 1000 --banners <target>
```

## rustscan

### Basic Usage
```bash
# Basic scan
rustscan -a <target>

# Specify ports
rustscan -a <target> -p 22,80,443

# Port range
rustscan -a <target> -r 1-1000

# All ports
rustscan -a <target> -r 1-65535
```

### Performance Options
```bash
# Batch size (default 4500)
rustscan -a <target> -b 1000

# Timeout (milliseconds)
rustscan -a <target> -t 2000

# Threads
rustscan -a <target> --ulimit 5000
```

### Integration with nmap
```bash
# Pass to nmap for service detection
rustscan -a <target> -- -sV

# Aggressive nmap scan
rustscan -a <target> -- -A

# Script scanning
rustscan -a <target> -- -sC
```

### Output Options
```bash
# JSON output
rustscan -a <target> -o json

# Normal output to file
rustscan -a <target> > rustscan.txt

# Grep-friendly output
rustscan -a <target> -g
```

### Advanced Features
```bash
# Multiple targets
rustscan -a <target1>,<target2>

# CIDR range
rustscan -a 192.168.1.0/24

# Read targets from file
rustscan -a targets.txt

# Custom user agent
rustscan -a <target> --user-agent "Mozilla/5.0"
```

### Common One-Liners
```bash
# Fast all ports with nmap service detection
rustscan -a <target> -r 1-65535 -- -sV

# Quick web scan
rustscan -a <target> -p 80,443,8080,8443 -- -sC

# Network range scan
rustscan -a 192.168.1.0/24 -p 22,80,443
```

## Port Scanning Strategy

### 1. Discovery Phase
```bash
# Host discovery
nmap -sn 192.168.1.0/24

# Quick port scan
rustscan -a <target> -r 1-1000
```

### 2. Comprehensive Scanning
```bash
# All TCP ports
rustscan -a <target> -r 1-65535

# Service detection on open ports
nmap -sV -p <open-ports> <target>
```

### 3. UDP Scanning
```bash
# Top UDP ports
nmap -sU --top-ports 1000 <target>

# Specific UDP services
nmap -sU -p 53,67,68,69,123,161,500 <target>
```

### 4. Service Enumeration
```bash
# Script scanning
nmap -sC -p <open-ports> <target>

# Vulnerability scanning
nmap --script vulners -p <open-ports> <target>
```
