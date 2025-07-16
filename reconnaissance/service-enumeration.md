# Service Enumeration

## enum4linux

### Basic Usage
```bash
# Basic enumeration
enum4linux <target>

# All enumeration (verbose)
enum4linux -a <target>

# Username enumeration
enum4linux -U <target>

# Share enumeration
enum4linux -S <target>

# Password policy enumeration
enum4linux -P <target>
```

### Specific Enumeration Options
```bash
# Get machine information
enum4linux -M <target>

# Get printer information
enum4linux -i <target>

# Get group information
enum4linux -G <target>

# RID cycling
enum4linux -r <target>

# OS information
enum4linux -o <target>
```

### Advanced Options
```bash
# Specify username/password
enum4linux -u <username> -p <password> <target>

# Use null session
enum4linux -n <target>

# Specify dictionary file for usernames
enum4linux -U -d <target>

# Verbose output
enum4linux -v <target>
```

### Common One-Liners
```bash
# Complete enumeration
enum4linux -a -M -l -d <target>

# Quick user and share enum
enum4linux -U -S <target>

# RID cycling with known user
enum4linux -u guest -p "" -r <target>
```

## smbclient

### Basic Connection
```bash
# List shares
smbclient -L <target>

# Connect to share
smbclient //<target>/<share>

# Connect with credentials
smbclient //<target>/<share> -U <username>

# Connect with password
smbclient //<target>/<share> -U <username>%<password>
```

### Anonymous Access
```bash
# Anonymous connection
smbclient //<target>/<share> -N

# Guest access
smbclient //<target>/<share> -U guest

# Null session
smbclient //<target>/IPC$ -N
```

### SMB Commands
```bash
# Inside smbclient session:
# List files
ls

# Download file
get <filename>

# Upload file
put <local-file> <remote-file>

# Download all files
mget *

# Change directory
cd <directory>

# Print working directory
pwd

# Create directory
mkdir <directory>

# Delete file
del <filename>
```

### Enumeration Commands
```bash
# List shares with null session
smbclient -L <target> -N

# Access IPC$ share
smbclient //<target>/IPC$ -N

# Access C$ share
smbclient //<target>/C$ -U <username>

# Access ADMIN$ share
smbclient //<target>/ADMIN$ -U <username>
```

### Recursive Operations
```bash
# Recursive download
smbclient //<target>/<share> -N -c "recurse ON; prompt OFF; mget *"

# List all files recursively
smbclient //<target>/<share> -N -c "recurse ON; ls"
```

### Common One-Liners
```bash
# Quick share enumeration
smbclient -L <target> -N

# Download all accessible files
smbclient //<target>/<share> -N -c "prompt OFF; recurse ON; mget *"

# Check for write access
echo "test" | smbclient //<target>/<share> -N -c "put - test.txt"
```

## snmpwalk

### Basic Usage
```bash
# Default community string (public)
snmpwalk -v2c -c public <target>

# Specify OID
snmpwalk -v2c -c public <target> <OID>

# SNMPv1
snmpwalk -v1 -c public <target>

# SNMPv3
snmpwalk -v3 -u <username> <target>
```

### Common OIDs
```bash
# System information
snmpwalk -v2c -c public <target> 1.3.6.1.2.1.1

# Network interfaces
snmpwalk -v2c -c public <target> 1.3.6.1.2.1.2.2.1.2

# Running processes
snmpwalk -v2c -c public <target> 1.3.6.1.2.1.25.4.2.1.2

# Installed software
snmpwalk -v2c -c public <target> 1.3.6.1.2.1.25.6.3.1.2

# TCP connections
snmpwalk -v2c -c public <target> 1.3.6.1.2.1.6.13.1.3

# User accounts
snmpwalk -v2c -c public <target> 1.3.6.1.4.1.77.1.2.25
```

### Community String Enumeration
```bash
# Common community strings
snmpwalk -v2c -c public <target>
snmpwalk -v2c -c private <target>
snmpwalk -v2c -c community <target>
snmpwalk -v2c -c manager <target>
```

### Advanced Options
```bash
# Increase timeout
snmpwalk -v2c -c public -t 10 <target>

# Increase retries
snmpwalk -v2c -c public -r 5 <target>

# Output numeric OIDs
snmpwalk -v2c -c public -On <target>

# Output values only
snmpwalk -v2c -c public -Oq <target>
```

### Common One-Liners
```bash
# System info
snmpwalk -v2c -c public <target> 1.3.6.1.2.1.1.1.0

# Process list
snmpwalk -v2c -c public <target> 1.3.6.1.2.1.25.4.2.1.2

# Network interfaces
snmpwalk -v2c -c public <target> 1.3.6.1.2.1.2.2.1.2
```

## FTP Enumeration

### Basic FTP Commands
```bash
# Connect to FTP
ftp <target>

# Anonymous login
ftp <target>
# Username: anonymous
# Password: anonymous

# List files
ls -la

# Download file
get <filename>

# Upload file
put <filename>

# Binary mode
binary

# Passive mode
passive
```

### FTP Banner Grabbing
```bash
# Netcat banner grab
nc <target> 21

# Telnet banner grab
telnet <target> 21

# Nmap script
nmap --script ftp-anon,ftp-bounce,ftp-proftpd-backdoor <target> -p 21
```

## SSH Enumeration

### SSH Banner Grabbing
```bash
# Netcat banner grab
nc <target> 22

# SSH version
ssh -V <target>

# Nmap scripts
nmap --script ssh-hostkey,ssh-auth-methods <target> -p 22
```

### SSH Brute Force
```bash
# Hydra SSH brute force
hydra -l <username> -P <wordlist> ssh://<target>

# Nmap brute force
nmap --script ssh-brute --script-args userdb=users.txt,passdb=passwords.txt <target> -p 22
```

## HTTP/HTTPS Enumeration

### HTTP Methods
```bash
# Options method
curl -X OPTIONS <target>

# HEAD method
curl -I <target>

# Check for dangerous methods
nmap --script http-methods <target> -p 80,443
```

### HTTP Headers
```bash
# Get headers
curl -I <target>

# Specific headers
curl -H "User-Agent: Mozilla/5.0" <target>

# Nmap script
nmap --script http-headers <target> -p 80,443
```

### SSL/TLS Enumeration
```bash
# SSL certificate info
openssl s_client -connect <target>:443

# SSL cipher enumeration
nmap --script ssl-enum-ciphers <target> -p 443

# SSL vulnerabilities
nmap --script ssl-heartbleed,ssl-poodle <target> -p 443
```

## LDAP Enumeration

### Basic LDAP Queries
```bash
# Anonymous bind
ldapsearch -x -h <target> -b "dc=domain,dc=com"

# Search for users
ldapsearch -x -h <target> -b "dc=domain,dc=com" "(objectclass=user)"

# Search for groups
ldapsearch -x -h <target> -b "dc=domain,dc=com" "(objectclass=group)"
```

### LDAP with Credentials
```bash
# Authenticated bind
ldapsearch -x -h <target> -D "cn=admin,dc=domain,dc=com" -w <password> -b "dc=domain,dc=com"

# Search for all objects
ldapsearch -x -h <target> -D "<user>" -w <password> -b "dc=domain,dc=com" "(objectclass=*)"
```

## RPC Enumeration

### RPCbind
```bash
# List RPC services
rpcinfo -p <target>

# Specific program
rpcinfo -p <target> | grep <program>

# NFS enumeration
showmount -e <target>
```

### RPC Endpoint Mapper
```bash
# Windows RPC
rpcclient -U "" <target>

# Inside rpcclient:
# Enumerate users
enumdomusers

# Enumerate groups
enumdomgroups

# Get user info
queryuser <username>
```

## Database Enumeration

### MySQL
```bash
# Connect to MySQL
mysql -h <target> -u <username> -p

# Nmap scripts
nmap --script mysql-enum,mysql-info <target> -p 3306
```

### PostgreSQL
```bash
# Connect to PostgreSQL
psql -h <target> -U <username> -d <database>

# Nmap scripts
nmap --script pgsql-brute <target> -p 5432
```

### MSSQL
```bash
# Nmap scripts
nmap --script ms-sql-info,ms-sql-config <target> -p 1433

# Connect with sqsh
sqsh -S <target> -U <username> -P <password>
```

## Service Enumeration Methodology

### 1. Port Identification
```bash
# Quick port scan
nmap -sS -T4 --top-ports 1000 <target>

# Service version detection
nmap -sV -p <open-ports> <target>
```

### 2. Service-Specific Enumeration
```bash
# SMB (ports 139, 445)
enum4linux -a <target>
smbclient -L <target> -N

# SNMP (port 161)
snmpwalk -v2c -c public <target>

# HTTP/HTTPS (ports 80, 443)
curl -I <target>
nmap --script http-enum <target> -p 80,443
```

### 3. Authentication Testing
```bash
# Test for anonymous/guest access
# Try default credentials
# Check for null sessions
```

### 4. Information Gathering
```bash
# Extract usernames, shares, configurations
# Identify software versions
# Look for sensitive information
```
