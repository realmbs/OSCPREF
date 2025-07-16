# OSCP Reference Repository

A comprehensive, searchable reference for OSCP preparation focusing on quick command syntax and flags.

## Table of Contents

- [OSCP Reference Repository](#oscp-reference-repository)
  - [Table of Contents](#table-of-contents)
  - [Quick Search Guide](#quick-search-guide)
  - [Repository Structure](#repository-structure)
    - [Directory Descriptions](#directory-descriptions)
  - [Getting Started](#getting-started)
  - [Contributing](#contributing)

## Quick Search Guide

- **GitHub Search**: Press `Ctrl+K` (or `Cmd+K` on Mac) anywhere in the repo to search all files
- **Browser Search**: Use `Ctrl+F` within any file to find specific commands or flags
- **Search Tips**: Use keywords like `nmap`, `gobuster`, `privilege escalation`, `windows`, `linux`, etc.

## Repository Structure

```
OSCPREF/
├── README.md                           # This file - main navigation hub
├── reconnaissance/
│   ├── network-scanning.md             # nmap, masscan, rustscan
│   ├── web-enumeration.md              # gobuster, dirb, ffuf, nikto
│   ├── service-enumeration.md          # enum4linux, smbclient, snmpwalk
│   └── dns-enumeration.md              # dig, host, dnsrecon, fierce
├── exploitation/
│   ├── metasploit.md                   # msfconsole, msfvenom, handlers
│   ├── web-exploitation.md             # SQLi, XSS, file upload, LFI/RFI
│   ├── buffer-overflow.md              # pattern creation, offset finding, shellcode
│   └── manual-exploitation.md          # nc, socat, reverse shells
├── post-exploitation/
│   ├── linux-privesc.md                # linpeas, pspy, sudo, SUID, capabilities
│   ├── windows-privesc.md              # winpeas, powershell, token manipulation
│   ├── persistence.md                  # backdoors, scheduled tasks, services
│   └── lateral-movement.md             # psexec, wmiexec, pass-the-hash
├── tools/
│   ├── burp-suite.md                   # Proxy, scanner, repeater shortcuts
│   ├── wireshark.md                    # Filters, analysis techniques
│   ├── john-hashcat.md                 # Password cracking syntax
│   └── steganography.md                # steghide, binwalk, strings
├── payloads/
│   ├── reverse-shells.md               # Various language reverse shells
│   ├── web-shells.md                   # PHP, ASP, JSP web shells
│   └── windows-payloads.md             # PowerShell, cmd, exe payloads
├── methodology/
│   ├── enumeration-checklist.md        # Step-by-step enumeration process
│   ├── privilege-escalation-checklist.md # Systematic privesc approach
│   └── reporting-templates.md          # OSCP report structure and templates
└── quick-reference/
    ├── port-reference.md               # Common ports and services
    ├── file-transfers.md               # Multiple file transfer methods
    ├── one-liners.md                   # Useful one-liner commands
    └── troubleshooting.md              # Common issues and solutions
```

### Directory Descriptions

- **📁 reconnaissance/** - Tools and techniques for information gathering and target enumeration
- **📁 exploitation/** - Attack vectors, payloads, and exploitation frameworks
- **📁 post-exploitation/** - Privilege escalation, persistence, and lateral movement techniques
- **📁 tools/** - Specific tool configurations, shortcuts, and usage guides
- **📁 payloads/** - Ready-to-use shells, payloads, and code snippets
- **📁 methodology/** - Systematic approaches, checklists, and reporting templates
- **📁 quick-reference/** - Fast lookup tables, one-liners, and troubleshooting guides

## Getting Started

1. **Clone the repository**: `git clone <repo-url>`
2. **Browse by category**: Navigate to the folder that matches your current task
3. **Search efficiently**: Use the search features mentioned above
4. **Bookmark frequently used commands**: Keep your most-used references handy

## Contributing

This is a living document. Feel free to:
- Add new commands and techniques
- Improve existing documentation
- Fix any errors or outdated information
- Suggest new categories or organization improvements

---