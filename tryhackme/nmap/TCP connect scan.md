- TCP Connect scan works by performing the three-way handshake with each target port in turn.
- In other words, Nmap tries to connect to each specified TCP port, and determines whether the service is open by the response it receives.
![[nmap1.png]]

- if Nmap sends a TCP request with the _SYN_ flag set to a **_closed_** port, the target server will respond with a TCP packet with the _RST_ (Reset) flag set. By this response, Nmap can establish that the port is closed.
![](https://i.imgur.com/vUQL9SK.png)

## Port is hidden behind a firewall
- Many firewalls are configured to simply **drop** incoming packets.
- Nmap sends a TCP SYN request, and receives nothing back. This indicates that the port is being protected by a firewall and thus the port is considered to be filtered.
- That said, it is very easy to configure a firewall to respond with a RST TCP packet.

**For example, in IPtables for Linux, a simple version of the command would be as follows:**
```bash
iptables -I INPUT -p tcp --dport <port> -j REJECT --reject-with tcp-reset
```
This can make it extremely difficult (if not impossible) to get an accurate reading of the target(s).
TCP scans perform a full three-way handshake with the target.

## Syntax
```bash
Usage: nmap [Scan Type(s)] [Options] {target specification}
```

## Example
```bash
┌──(hyok㉿kali)-[~]
└─$ nmap -sT 192.168.1.9 
```