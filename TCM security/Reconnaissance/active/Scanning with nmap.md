### netdiscover
- it can passively detect online hosts, or search for them, by actively sending ARP requests. Netdiscover can also be used to inspect your network ARP traffic. 
- Netdiscover uses the OUI table to show the vendor of the each MAC address discovered. 
- Netdiscover is an active/passive address reconnaissance tool. 

### Installing netdiscover
```bash
┌──(hyok㉿kali)-[~]
└─$ sudo apt install netdiscover
```

### help menu
```bash
┌──(hyok㉿kali)-[~]
└─$ netdiscover -h
```

### Scanning a range of network
```bash
┌──(hyok㉿kali)-[~]
└─$ sudo netdiscover -r 192.168.216.0/24
```

### Arp-scan 
1. Scan the local network, using the information from the primary network interface:
```python
┌──(hyok㉿kali)-[~/Documents/hacking_notes]
└─$ sudo arp-scan -l
```

2. Scan a subnet, specifying the interface to use and a custom source MAC address:
```python
┌──(hyok㉿kali)-[~/Documents/hacking_notes]
└─$ sudo arp-scan -I eth0 --srcaddr=08:00:27:1a:7c:43 192.168.1.0/24
```

## nmap
1. Scanning an entire ports(0-65365) and all of the services
```python
┌──(hyok㉿kali)-[~/Documents/hacking_notes]
└─$ sudo nmap -T4 -p- -A 192.168.1.7
```
