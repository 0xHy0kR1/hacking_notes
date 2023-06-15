- UDP connections are stateless. This means that, UDP connections rely on sending packets to a target port and essentially hoping that they make it.
- This makes UDP superb for connections which rely on speed over quality (e.g. video sharing), but the lack of acknowledgement makes UDP significantly more difficult (and much slower) to scan.
- The switch for an Nmap UDP scan is (`-sU`).

## Working
- When a packet is sent to an open UDP port, there should be no response. When this happens, Nmap refers to the port as being `open|filtered`. 
	- In other words, it suspects that the port is open, but it could be firewalled.
	- If it gets a UDP response (which is very unusual), then the port is marked as _open_.
- When a packet is sent to a _closed_ UDP port, the target should respond with an ICMP (ping) packet containing a message that the port is unreachable.
	- This clearly identifies closed ports.

**Note** - it's usually good practice to run an Nmap scan with `--top-ports <number>` enabled because UDP scans are slow as compare to TCP scans. nmap sends raw UDP packets, when scanning with UDP ports.

## Syntax
```bash
nmap -sU --top-ports 20 <target>
```
