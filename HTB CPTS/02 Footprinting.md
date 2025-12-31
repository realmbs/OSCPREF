# FTP (TCP/21, TCP/20)
footprint FTP w/ nmap scripts ftp-anon, ftp-syst

p21: control
p20: data transmission

file transfer protocol
cleartext protocol
runs within application layer of TCP/IP stack (same layer as HTTP & POP)

active FTP: client transmits port to server for communication
passive FTP: server announces a port to client for communication

# TFTP (UDP/69)
trivial file transfer protocol
simpler than FTP
does not provide auth
uses UDP (less reliable)

## TFTP commands
| command | description |
| connect | sets remote host, port optional for file transfers | 
| get | transfers file / files from remote host to local host |
| put | transfers file / files from local host to remote host |
| quit | exits |
| status | shows current status, transfer mode, connection status, timeout value |

frequently used Linux FTP server: vsFTPd

default conf = /etc/vsftpd.conf
/etc/ftpusers

# SMB (TCP/139, TCP/445)
nmap (-p139,445)
rpcclient -U "" <ip>
| query | description |
| srvinfo | server info |
| enumdomains | enumerate all domains |
| querydominfo | pull domain, server, user info |
| netshareenumall | enumerate all shares |
| netsharegetinfo <share> | pull info about specific share |
| enumdomusers | enumerate all users |
| queryuser <RID> | pull info about specific user |

## rpcclient methodology
enumeration
1. srvinfo
2. enumdomains
3. querydominfo
4. netshareenumall
5. netsharegetinfo <share>

user enumeration
1. enumdomusers
2. queryuser <RID>
3. querygroup <RID>

## brute forcing RIDs
bash method
$ for i in $(seq 500 1100); do rpcclient -N -U "" <ip> -c "queryuser 0x$(printf '%x\n' $i)" | grep "User Name\|user_rid\|group_rid" && echo "" ;done

python method: samrdump.py
samrdump.py <ip>

## SMBmap
smbmap -H <ip>

## CrackMapExec
crackmapexec smb <ip> --shares -u '' -p ''

## enum4linux-ng
https://github.com/cddmp/enum4linux-ng.git
./enum4linux-ng.py <ip> -A

## **connect to SMB - smbclient method**
smbclient -N -L //<ip>
smbclient //<ip>/<share>

# NFS