# flags
-sS
nmap -sS 192.168.1.1
basic SYN scan
returns: open, closed, filtered

-sn
nmap -sn 192.168.1.0/24
nmap -sn 192.168.1.10-128
disables port scanning
used to scan network ranges

-iL
nmap -sn -iL hosts.lst
input a .lst formatted hosts list

