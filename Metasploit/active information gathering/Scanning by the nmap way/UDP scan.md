# Pre-requisite - [[Beginning nmap]]
- The UDP scan [-sU] is the scanning technique to identify open UDP ports on the target.
- UDP scanning is a connectionless scanning technique; hence, no notification is sent back to the scanner, whether the packet has been received by the target or not.
# Code - 
```python
msf6 > nmap -sU 192.168.216.4
[*] exec: nmap -sU 192.168.216.4

Starting Nmap 7.93 ( https://nmap.org ) at 2023-02-22 14:38 IST
Nmap scan report for 192.168.216.4 (192.168.216.4)
Host is up (0.00055s latency).
Not shown: 993 closed udp ports (port-unreach)
PORT     STATE         SERVICE
53/udp   open          domain
68/udp   open|filtered dhcpc
69/udp   open|filtered tftp
111/udp  open          rpcbind
137/udp  open          netbios-ns
138/udp  open|filtered netbios-dgm
2049/udp open          nfs
MAC Address: 08:00:27:EC:47:BA (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 1109.07 seconds
```
# Some extra information - 
- If the port is closed, then an ICMP port unreachable message is sent back to the scanner. If no message is received, then the port is reported as open.
- This method can return false results as firewalls can block the data packets and, therefore, no response message will be generated and the scanner will report the port as open.