# Pre-requisite - [[Beginning nmap]]
- The TCP connect [-sT] scan is the most basic and default scan type in Nmap.
- It follows the three-way handshake process to detect the open ports on the target machine. hence, the returned results of this scan are considered accurate.
# Code - 
```python
msf6 > nmap -sT 192.168.216.4
[*] exec: nmap -sT 192.168.216.4

Starting Nmap 7.93 ( https://nmap.org ) at 2023-02-22 13:54 IST
Nmap scan report for 192.168.216.4 (192.168.216.4)
Host is up (0.00046s latency).
Not shown: 977 closed tcp ports (conn-refused)
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
23/tcp   open  telnet
25/tcp   open  smtp
53/tcp   open  domain
80/tcp   open  http
111/tcp  open  rpcbind
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
512/tcp  open  exec
513/tcp  open  login
514/tcp  open  shell
1099/tcp open  rmiregistry
1524/tcp open  ingreslock
2049/tcp open  nfs
2121/tcp open  ccproxy-ftp
3306/tcp open  mysql
5432/tcp open  postgresql
5900/tcp open  vnc
6000/tcp open  X11
6667/tcp open  irc
8009/tcp open  ajp13
8180/tcp open  unknown
MAC Address: 08:00:27:EC:47:BA (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 0.42 seconds
```
# Some extra information - 
- The TCP connect scan is the most basic scanning technique in which a full connection is established with the port under test. 
- It uses the operating system's network functions to establish connections.
- The scanner sends a SYN packet to the target machine. If the port is open, it returns an ACK message back to the scanner. The scanner then sends an ACK packet back to the target showing the successful establishment of a connection.
- This technique has its benefits, but it is easily traceable by firewalls and IDS.
