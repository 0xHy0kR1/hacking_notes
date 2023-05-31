# pre-requisite - [[Configuring the PostgreSQL database for metasploit]]
# pre-requisite - [[Active information gathering]]
- ARP Sweep allows us to enumerate live hosts in the local network using ARP requests, providing us with a simple and fast way to identify possible targets
- When your target systems are located on the same LAN as your attacking machine, you are able to enumerate systems by performing an ARP scan.
# Code - 
```python
msf6 > use auxiliary/scanner/discovery/arp_sweep
msf6 auxiliary(scanner/discovery/arp_sweep) > set RHOSTS 192.168.216.0/24
RHOSTS => 192.168.216.0/24
msf6 auxiliary(scanner/discovery/arp_sweep) > set THREADS 256 
THREADS => 256
msf6 auxiliary(scanner/discovery/arp_sweep) > run

[+] 192.168.216.1 appears to be up (Realtek (UpTech? also reported)).
[+] 192.168.216.2 appears to be up (Realtek (UpTech? also reported)).
[+] 192.168.216.3 appears to be up (CADMUS COMPUTER SYSTEMS).
[+] 192.168.216.7 appears to be up (CADMUS COMPUTER SYSTEMS).
[*] Scanned 256 of 256 hosts (100% complete)
[*] Auxiliary module execution completed
```
# Some extra information - 
#### If enabled, the results will be stored in the Metasploit database. To display the hosts discovered, you can use the hosts command:
```python
msf6 auxiliary(scanner/discovery/arp_sweep) > hosts

Hosts
=====

address          mac              name            os_name       os_flavor  os_sp  purpose  info  comments
-------          ---              ----            -------       ---------  -----  -------  ----  --------
192.168.216.1    52:54:00:12:35:
                 00
192.168.216.2    52:54:00:12:35:
                 00
192.168.216.3    08:00:27:7f:2f:
                 29
192.168.216.7    08:00:27:f9:15:  192.168.216.7   Windows 2008                    server
                 a6
192.168.216.10   08:00:27:b3:84:  192.168.216.10  Windows 7                       client
                 74
2400:cb00:2049:
1::adf5:3a33
2400:cb00:2049:
1::adf5:3b29
2400:cb00:2049:
1::c629:dead
2606:4700::6810
:f34e
2606:4700::6810
:f44e
```