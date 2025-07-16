# DNS Enumeration

## dig

### Basic Queries
```bash
# Basic A record lookup
dig <domain>

# Specific record type
dig <domain> A
dig <domain> AAAA
dig <domain> MX
dig <domain> NS
dig <domain> TXT
dig <domain> SOA
dig <domain> CNAME

# Query specific DNS server
dig @<dns-server> <domain>

# Short output
dig +short <domain>
```

### Zone Transfers
```bash
# Attempt zone transfer
dig @<nameserver> <domain> AXFR

# Find nameservers first
dig <domain> NS

# Try zone transfer on each nameserver
dig @ns1.domain.com domain.com AXFR
dig @ns2.domain.com domain.com AXFR
```

### Reverse DNS Lookups
```bash
# Reverse lookup
dig -x <ip-address>

# PTR record
dig <reverse-ip>.in-addr.arpa PTR

# IPv6 reverse lookup
dig -x <ipv6-address>
```

### Advanced Options
```bash
# Trace DNS resolution path
dig +trace <domain>

# No recursion
dig +norecurse <domain>

# Include additional information
dig +additional <domain>

# Query all record types
dig <domain> ANY

# Verbose output
dig +verbose <domain>
```

### Common One-Liners
```bash
# Quick subdomain check
dig +short <subdomain>.<domain>

# Mail servers
dig +short <domain> MX

# Name servers
dig +short <domain> NS

# All TXT records
dig <domain> TXT +short
```

## host

### Basic Usage
```bash
# Basic lookup
host <domain>

# Specific record type
host -t A <domain>
host -t MX <domain>
host -t NS <domain>
host -t TXT <domain>
host -t SOA <domain>

# Reverse lookup
host <ip-address>

# Query specific DNS server
host <domain> <dns-server>
```

### Zone Transfers
```bash
# Attempt zone transfer
host -l <domain> <nameserver>

# All record types
host -a <domain>

# Verbose output
host -v <domain>
```

### Advanced Options
```bash
# Disable recursive queries
host -R <domain>

# Specify query class
host -c IN <domain>

# Set timeout
host -W <seconds> <domain>

# Debug mode
host -d <domain>
```

### Common One-Liners
```bash
# Quick MX lookup
host -t MX <domain>

# Find all subdomains via zone transfer
host -l <domain> <nameserver>

# Reverse lookup range
for ip in {1..254}; do host 192.168.1.$ip; done
```

## dnsrecon

### Basic Usage
```bash
# Standard enumeration
dnsrecon -d <domain>

# Specific record types
dnsrecon -d <domain> -t A,MX,NS,TXT

# Zone transfer attempt
dnsrecon -d <domain> -t axfr

# Reverse lookup
dnsrecon -r <ip-range>
```

### Subdomain Enumeration
```bash
# Brute force subdomains
dnsrecon -d <domain> -t brt

# Custom wordlist
dnsrecon -d <domain> -t brt -D <wordlist>

# Google enumeration
dnsrecon -d <domain> -t goo

# Bing enumeration
dnsrecon -d <domain> -t bing
```

### Advanced Features
```bash
# Cache snooping
dnsrecon -d <domain> -t snoop

# SRV record enumeration
dnsrecon -d <domain> -t srv

# TLD expansion
dnsrecon -d <domain> -t tld

# Wildcard detection
dnsrecon -d <domain> -t wildcard
```

### Output Options
```bash
# XML output
dnsrecon -d <domain> -x <output.xml>

# JSON output
dnsrecon -d <domain> -j <output.json>

# CSV output
dnsrecon -d <domain> -c <output.csv>
```

### Common One-Liners
```bash
# Full enumeration
dnsrecon -d <domain> -t std,brt,srv,axfr

# Subdomain brute force with custom list
dnsrecon -d <domain> -t brt -D /usr/share/wordlists/dnsmap.txt

# Network range reverse lookup
dnsrecon -r 192.168.1.0/24
```

## fierce

### Basic Usage
```bash
# Basic scan
fierce --domain <domain>

# Specify DNS servers
fierce --dns-servers <dns-server> --domain <domain>

# Custom wordlist
fierce --wordlist <wordlist> --domain <domain>

# Subdomain enumeration
fierce --subdomain-file <subdomains.txt> --domain <domain>
```

### Advanced Options
```bash
# Delay between requests
fierce --delay <seconds> --domain <domain>

# Search nearby IPs
fierce --range <ip-range> --domain <domain>

# Connect timeout
fierce --connect-timeout <seconds> --domain <domain>

# Wide scan (more comprehensive)
fierce --wide --domain <domain>
```

### Output Options
```bash
# Save results to file
fierce --domain <domain> > fierce_results.txt

# Combine with other tools
fierce --domain <domain> | grep "Found:"
```

### Common One-Liners
```bash
# Quick subdomain scan
fierce --domain <domain>

# Comprehensive scan with custom wordlist
fierce --domain <domain> --wordlist /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt

# Wide scan with delay
fierce --domain <domain> --wide --delay 1
```

## nslookup

### Basic Usage
```bash
# Interactive mode
nslookup
> <domain>
> set type=MX
> <domain>

# Non-interactive mode
nslookup <domain>
nslookup <domain> <dns-server>

# Specific record types
nslookup -type=A <domain>
nslookup -type=MX <domain>
nslookup -type=NS <domain>
nslookup -type=TXT <domain>
```

### Advanced Queries
```bash
# Reverse lookup
nslookup <ip-address>

# Debug mode
nslookup -debug <domain>

# Query class
nslookup -class=IN <domain>

# Port specification
nslookup -port=53 <domain>
```

## DNS Brute Force Tools

### gobuster DNS
```bash
# Basic DNS brute force
gobuster dns -d <domain> -w <wordlist>

# Show IP addresses
gobuster dns -d <domain> -w <wordlist> -i

# Specify resolvers
gobuster dns -d <domain> -w <wordlist> -r <resolver-file>

# Timeout settings
gobuster dns -d <domain> -w <wordlist> -t 50 --timeout 10s
```

### amass
```bash
# Basic enumeration
amass enum -d <domain>

# Passive enumeration only
amass enum -passive -d <domain>

# Active enumeration
amass enum -active -d <domain>

# Brute force
amass enum -brute -d <domain>

# Output to file
amass enum -d <domain> -o amass_results.txt
```

### subfinder
```bash
# Basic subdomain enumeration
subfinder -d <domain>

# Silent mode (only subdomains)
subfinder -d <domain> -silent

# Use all sources
subfinder -d <domain> -all

# Output to file
subfinder -d <domain> -o subdomains.txt
```

## DNS Zone Walking

### Basic Zone Walking
```bash
# Using dnsrecon
dnsrecon -d <domain> -t zonewalk

# Using dig with NSEC records
dig <domain> NSEC

# Walking DNSSEC zones
dig <domain> NSEC3PARAM
```

## DNS Cache Poisoning Detection

### Cache Snooping
```bash
# Using dnsrecon
dnsrecon -d <domain> -t snoop -D <wordlist>

# Manual cache snooping
dig @<dns-server> <domain> +norecurse
```

## DNS over HTTPS/TLS

### DNS over HTTPS
```bash
# Using curl
curl -H 'accept: application/dns-json' 'https://cloudflare-dns.com/dns-query?name=<domain>&type=A'

# Using dig with DoH
dig @https://cloudflare-dns.com/dns-query <domain>
```

### DNS over TLS
```bash
# Using kdig
kdig @853 +tls-ca <domain>

# Using dig with DoT
dig @1.1.1.1 -p 853 +tcp <domain>
```

## DNS Enumeration Automation

### All-in-One Script
```bash
#!/bin/bash
domain=$1

echo "=== DNS Enumeration for $domain ==="

echo "--- Basic DNS Records ---"
dig $domain A +short
dig $domain AAAA +short
dig $domain MX +short
dig $domain NS +short
dig $domain TXT +short

echo "--- Zone Transfer Attempts ---"
for ns in $(dig $domain NS +short); do
    echo "Trying zone transfer on $ns"
    dig @$ns $domain AXFR
done

echo "--- Subdomain Enumeration ---"
dnsrecon -d $domain -t brt -D /usr/share/wordlists/dnsmap.txt

echo "--- Reverse DNS ---"
for ip in $(dig $domain A +short); do
    dig -x $ip +short
done
```

## DNS Enumeration Methodology

### 1. Basic Information Gathering
```bash
# Get basic records
dig <domain> A MX NS TXT SOA

# Identify name servers
dig <domain> NS +short
```

### 2. Zone Transfer Testing
```bash
# Test each name server
for ns in $(dig <domain> NS +short); do
    dig @$ns <domain> AXFR
done
```

### 3. Subdomain Enumeration
```bash
# Multiple approaches
dnsrecon -d <domain> -t brt
gobuster dns -d <domain> -w <wordlist>
amass enum -d <domain>
```

### 4. Reverse DNS Analysis
```bash
# Check IP ranges
dnsrecon -r <ip-range>

# Manual reverse lookups
dig -x <ip>
```

### 5. Advanced Techniques
```bash
# DNSSEC analysis
dig <domain> DNSKEY
dig <domain> DS

# Cache analysis
dnsrecon -d <domain> -t snoop
```

## Common DNS Wordlists

### Built-in Wordlists
```bash
# SecLists
/usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt
/usr/share/seclists/Discovery/DNS/dns-Jhaddix.txt

# DNSMap
/usr/share/wordlists/dnsmap.txt

# Fierce
/usr/share/fierce/hosts.txt
```

### Custom Wordlist Creation
```bash
# Extract subdomains from certificates
curl -s "https://crt.sh/?q=%.<domain>&output=json" | jq -r '.[].name_value' | sort -u

# From Google dorks
site:<domain> -www

# From Wayback Machine
curl -s "http://web.archive.org/cdx/search/cdx?url=*.<domain>/*&output=text&fl=original&collapse=urlkey"
```
