## NULL(-sN) scan 
- NULL scans (`-sN`) are when the TCP request is sent with no flags set at all.
- As per the RFC, the target host should respond with a RST if the port is closed.
![[nmap3.png]]

#### Example
```python
┌──(hyok㉿kali)-[~/Downloads]
└─$ sudo nmap -sN  192.168.1.9
```

## FIN(-sF) scan
- instead of sending a completely empty packet, a request is sent with the FIN flag (usually used to gracefully close an active connection).
- Nmap expects a RST if the port is closed.
![[nmap4.png]]

#### Example
```python
┌──(hyok㉿kali)-[~/Downloads]
└─$ sudo nmap -sF  192.168.1.9 
```

## Xmas(-sX) scan 
- Xmas scans (`-sX`) send a malformed TCP packet and expects a RST response for closed ports.
- If the port is open then there is no response to the malformed packet.
- RFC 793 mandates that network hosts respond to malformed packets with a RST TCP packet for closed ports, and don't respond at all for open ports
![[nmap5.png]]

#### Example
```python
┌──(hyok㉿kali)-[~/Downloads]
└─$ sudo nmap -sX  192.168.1.9
```

If a port is identified as filtered with one of these scans then it is usually because the target has responded with an ICMP unreachable packet.
