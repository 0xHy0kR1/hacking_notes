- SYN scans (`-sS`) are used to scan the TCP port-range of a target or targets.
- SYN scans are sometimes referred to as "Half-open" scans, or "Stealth" scans.
- SYN scans sends back a RST TCP packet after receiving a SYN/ACK from the server. In other words, the sequence for scanning an **open** port looks like this:
![[nmap2.png]]

### This has a variety of advantages for us as hackers:
- It can be used to bypass older Intrusion Detection systems as they are looking out for a full three way handshake. This is often no longer the case with modern IDS solutions.
- SYN scans are significantly faster than a standard TCP Connect scan.

### There are, however, a couple of disadvantages to SYN scans, namely:
- They require sudo permissions[1] in order to work correctly in Linux. This is because SYN scans require the ability to create raw packets (as opposed to the full TCP handshake)
- Unstable services are sometimes brought down by SYN scans.

**Note** - SYN scans are the default scans used by Nmap if run with sudo permissions. If run **without** sudo permissions, Nmap defaults to the TCP Connect scan.

## Syntax
```bash
Usage: nmap [Scan Type(s)] [Options] {target specification}
```

## Example
```bash
┌──(hyok㉿kali)-[~]
└─$ sudo nmap -sS 192.168.1.9
```