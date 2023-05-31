- The firewall and IDS logs can reveal your IP address if you perform a scan without using security measures. One such feature is provided in Nmap, called decoy (-D).
- The decoy option does not prevent your IP address from getting recorded in the log file of firewalls and IDS, but it does make the scan look scary.
- It adds other torrents in the log files, thus creating an impression that there are several other attackers scanning the machine simultaneously. So, if you add two decoy IP addresses, the log file will show that the request packets were sent from three different IP addresses; one will be yours and the other two will be the fake addresses added by you:
```python
msf6 > nmap -sT 192.168.216.4 -D 192.168.216.13,192.168.216.25
[*] exec: nmap -sT 192.168.216.4 -D 192.168.216.13,192.168.216.25

Starting Nmap 7.93 ( https://nmap.org ) at 2023-02-22 15:18 IST
You have specified some options that require raw socket access.
These options will not be honored for TCP Connect scan.
Nmap scan report for 192.168.216.4 (192.168.216.4)
Host is up (0.00086s latency).
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

Nmap done: 1 IP address (1 host up) scanned in 0.35 seconds
```
# Some extra information - 
- The IP addresses after the -D operator are the fake IP addresses, which will also appear in the network log files of the target machine, along with the original IP address.
- But adding too many decoy addresses can affect the scan results; hence, you should use a limited number of decoy addresses only.