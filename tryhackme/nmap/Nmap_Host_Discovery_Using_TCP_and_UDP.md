## TCP SYN Ping
   - If you want Nmap to use TCP SYN ping, you can do so via the option `-PS` followed by the port number, range, list, or a combination of them.
   - For example, `-PS21` will target port 21, while `-PS21-25` will target ports 21, 22, 23, 24, and 25. Finally `-PS80,443,8080` will target the three ports 80, 443, and 8080.
![[nmap18.png]]

   - Privileged users (root and sudoers) can send TCP SYN packets and don’t need to complete the TCP 3-way handshake even if the port is open.
   - Unprivileged users have no choice but to complete the 3-way handshake if the port is open.

**Command** - 
```python
nmap -PS -sn MACHINE_IP/24
```

![[nmap19.png]]

## TCP ACK Ping
   - You must be running Nmap as a privileged user to be able to accomplish this. If you try it as an unprivileged user, Nmap will attempt a 3-way handshake.
   - By default, port 80 is used. `-PA` should be followed by a port number, range, list, or a combination of them. For example, consider `-PA21`, `-PA21-25` and `-PA80,443,8080`. If no port is specified, port 80 will be used.
   - The target responds with the RST flag set because the TCP packet with the ACK flag is not part of any ongoing connection. The expected response is used to detect if the target host is up.
![[nmap20.png]]

**Command** - 
```python
sudo nmap -PA -sn MACHINE_IP/24
```

![[nmap21.png]]

## UDP ping
   - Contrary to TCP SYN ping, sending a UDP packet to an open port is not expected to lead to any reply. However, if we send a UDP packet to a closed UDP port, we expect to get an ICMP port unreachable packet; this indicates that the target system is up and available.

**In the following figure, we see a UDP packet sent to an open UDP port and not triggering any response. However, sending a UDP packet to any closed UDP port can trigger a response indirectly indicating that the target is online**
![[nmap22.png]]

**In the following example, we use a UDP scan, and we discover five live hosts.**
![[nmap23.png]]

## Masscan
   - On a side note, Masscan uses a similar approach to discover the available systems. However, to finish its network scan quickly, Masscan is quite aggressive with the rate of packets it generates.
**Examples** - 
```python
masscan MACHINE_IP/24 -p443
masscan MACHINE_IP/24 -p80,443
masscan MACHINE_IP/24 -p22-25
masscan MACHINE_IP/24 ‐‐top-ports 100
```

##### Notes - 
1. By default, Nmap will look up online hosts; however, you can use the option `-R` to query the DNS server even for offline hosts. 
2. If you want to use a specific DNS server, you can add the `--dns-servers DNS_SERVER` option.

