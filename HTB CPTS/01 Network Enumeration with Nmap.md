# nmap methodology
perform quick, less intrusive scan first
-> generates less traffic, faster
perform complete scan in background, enumerate services and version info

# nmap flags and their use
-sS
basic TCP SYN scan, does not complete 3 way handshake
more stealthy technique but less accurate than -sT scan
returns: open, closed, filtered
scans top 1000

-sT
TCP connect scan, completes 3 way handshake (more accurate than SYN scan)
one of the loudest techniques, easily detected by IDS/IPS

-sA
TCP ACK scan
harder for firewalls and IDS/IPS to filter than -sS SYN scan or -sT TCP connect scan

-sn
nmap -sn 192.168.1.0/24
nmap -sn 192.168.1.10-128
disables port scanning
used to scan network ranges

-iL
nmap -sn -iL hosts.lst
input a .lst formatted hosts list

--packet-trace

--disable-arp-ping
disables ARP ping

-sU
UDP scan, very slow due to UDP being stateless protocol

-sV
version and service scan 

-O
operating system detection

-e <tun0>
specify exit interface

--source-port <53>
(TCP/53 => DNS)
since DNS servers can be more trusted, this method can be used when working inside DMZ

-p-
nmap -sS 192.168.1.1 -p-
scans all ports

-oA
nmap -sS 192.168.1.1. -oA output
stores results in all formats (.gnmap, .xml, .nmap), filename starts with output

-oN
nmap -sS 192.168.1.1. -oN output
stores results as output.nmap

-oG
nmap -sS 192.168.1.1. -oG output
stores results in output.gnmap (greppable)

-oX
nmap -sS 192.168.1.1. -oX output
stores results in output.xml

-v
verbose output

-F
top 100 ports

-T <0-5>
timing / agressiveness

-D RND:<5>
decoy method, nmap generates random IPs and inserts them into IP header
nmap -sS -T4 192.168.1.1 -D RND:5