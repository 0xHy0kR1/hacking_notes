- The UDP Service Sweeper auxiliary module allows us to detect interesting UDP services.
- Since UDP is a connectionless protocol, it is more difficult to probe than TCP.
# Code - 
```python
msf6 auxiliary(scanner/discovery/arp_sweep) > use auxiliary/scanner/discovery/udp_sweep
msf6 auxiliary(scanner/discovery/udp_sweep) > set RHOSTS 192.168.216.0/24
RHOSTS => 192.168.216.0/24
msf6 auxiliary(scanner/discovery/udp_sweep) > run
[*] Sending 13 probes to 192.168.216.0->192.168.216.255 (256 hosts)
[*] Discovered NetBIOS on 192.168.216.4:137 (METASPLOITABLE:<00>:U :METASPLOITABLE:<03>:U :METASPLOITABLE:<20>:U :WORKGROUP:<00>:G :WORKGROUP:<1e>:G :00:00:00:00:00:00)
[*] Discovered Portmap on 192.168.216.4:111 (100000 v2 TCP(111), 100000 v2 UDP(111), 100024 v1 UDP(54265), 100024 v1 TCP(55287), 100003 v2 UDP(2049), 100003 v3 UDP(2049), 100003 v4 UDP(2049), 100021 v1 UDP(58592), 100021 v3 UDP(58592), 100021 v4 UDP(58592), 100003 v2 TCP(2049), 100003 v3 TCP(2049), 100003 v4 TCP(2049), 100021 v1 TCP(33417), 100021 v3 TCP(33417), 100021 v4 TCP(33417), 100005 v1 UDP(47926), 100005 v1 TCP(37458), 100005 v2 UDP(47926), 100005 v2 TCP(37458), 100005 v3 UDP(47926), 100005 v3 TCP(37458))
[*] Discovered DNS on 192.168.216.4:53 (BIND 9.4.2)
[*] Scanned 256 of 256 hosts (100% complete)
[*] Auxiliary module execution completed
```