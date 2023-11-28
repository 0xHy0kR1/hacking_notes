## NULL(-sN) scan 
- NULL scans (`-sN`) are when the TCP request is sent with no flags set at all.
- As per the RFC, the target host should respond with a RST if the port is closed.
![[nmap3.png]]

![[nmap26.png]]

![[nmap27.png]]

#### Example
```python
┌──(hyok㉿kali)-[~/Downloads]
└─$ sudo nmap -sN  192.168.1.9
```

## FIN(-sF) scan
- instead of sending a completely empty packet, a request is sent with the FIN flag (usually used to gracefully close an active connection).
- Nmap expects a RST if the port is closed.
![[nmap4.png]]

![[nmap28.png]]

![[nmap29.png]]

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

![[nmap30.png]]

![[nmap31.png]]

#### Example
```python
┌──(hyok㉿kali)-[~/Downloads]
└─$ sudo nmap -sX  192.168.1.9
```

If a port is identified as filtered with one of these scans then it is usually because the target has responded with an ICMP unreachable packet.

#### Note
   - Adding `-sV` to your Nmap command will collect and determine service and version information for the open ports.
   - You can control the intensity with `--version-intensity LEVEL` where the level ranges between 0, the lightest, and 9, the most complete.
   - `-sV --version-light` has an intensity of 2, while `-sV --version-all` has an intensity of 9.
   - Stealth SYN scan `-sS` is not possible when `-sV` option is chosen.
   - `-sV` required connecting to this open port to grab the service banner and any version information it can get, such as `nginx 1.6.2`.
   - If you want Nmap to find the routers between you and the target, just add `--traceroute`
