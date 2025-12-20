# nmap flags and their use
-sS
nmap -sS 192.168.1.1
basic TCP SYN scan, does not complete 3 way handshake
more stealthy technique but less accurate than -sT scan
returns: open, closed, filtered
scans top 1000

-sn
nmap -sn 192.168.1.0/24
nmap -sn 192.168.1.10-128
disables port scanning
used to scan network ranges

-iL
nmap -sn -iL hosts.lst
input a .lst formatted hosts list

--packet-trace
nmap 192.168.1.1 -p21 --packet-trace

-sT
nmap -sT 192.168.1.1 -p443
TCP connect scan, completes 3 way handshake (more accurate than SYN scan)
one of the loudest techniques, easily detected by IDS/IPS

-sU
nmap -sU 192.168.1.1
UDP scan, very slow due to UDP being stateless protocol

-sV
nmap -sS 192.168.1.1. -p445 -sV
version and service scan 