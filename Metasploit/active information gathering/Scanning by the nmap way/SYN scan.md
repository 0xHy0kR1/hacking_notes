# Pre-requisite - [[Beginning nmap]]
- The SYN scan [-sS] is considered a stealth scanning technique, as it never forms a complete connection between the target and the scanner.
- it is also called half-open scanning.
- The output of both TCP connect and the SYN scan are similar in most of the cases, but the only difference lies in the fact that SYN scans are difficult to detect by firewalls and Intrusion Detection Systems (IDS). However, modern firewalls are capable enough to catch SYN scans, as well.
# Code - 
```python
msf6 > nmap -sS 192.168.216.4
[*] exec: nmap -sS 192.168.216.4

Starting Nmap 7.93 ( https://nmap.org ) at 2023-02-22 14:30 IST
Nmap scan report for 192.168.216.4 (192.168.216.4)
Host is up (0.00087s latency).
Not shown: 977 closed tcp ports (reset)
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

Nmap done: 1 IP address (1 host up) scanned in 0.44 seconds
```
# Some extra information - 
- The –p parameter shows the range of port numbers that we want to scan. Using -p 0-65535, or -p - for short, will scan all the available ports.
- A SYN scan is another type of TCP scan, but it never forms a complete connection with the target. It doesn't use the operating system's network functions; instead, it generates raw IP packets and monitors for responses. If the port is open, then the target will respond with an ACK message.
- The scanner then sends a reset connection (RST) message and ends the connection.