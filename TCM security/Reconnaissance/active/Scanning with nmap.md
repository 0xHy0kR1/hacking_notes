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
  