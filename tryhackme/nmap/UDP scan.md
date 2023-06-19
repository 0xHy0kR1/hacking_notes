- UDP connections are _stateless_.
- This means that, UDP connections rely on sending packets to a target port and essentially hoping that they make it.
- When a packet is sent to an open UDP port, there should be no response. When this happens, Nmap refers to the port as being `open|filtered`.
- In other words, it suspects that the port is open, but it could be firewalled. If it gets a UDP response (which is very unusual), then the port is marked as _open_.
- When a packet is sent to a _closed_ UDP port, the target should respond with an ICMP (ping) packet containing a message that the port is unreachable.
- it's usually good practice to run an Nmap scan with `--top-ports <number>` enabled.
- When scanning UDP ports, Nmap usually sends completely empty requests -- just raw UDP packets.

## Syntax:
```bash
Usage: nmap [Scan Type(s)] [Options] {target specification}
```

## Example:
```python
┌──(hyok㉿kali)-[~/Downloads]
└─$ sudo nmap -sU 192.168.1.9
```