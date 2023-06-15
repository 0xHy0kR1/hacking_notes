- Traceroute can be used to map the path your request takes as it heads to the target machine.
- it allows you to see every intermediate step between your computer and the resource that you requested.

## Syntax
```bash
traceroute <destination>
```

- By default, the Windows traceroute utility (`tracert`) operates using the same ICMP protocol that ping utilises, and the Unix equivalent operates over UDP.

## Example
```bash
┌──(hyok㉿kali)-[~/Downloads]
└─$ traceroute 192.168.1.9
traceroute to 192.168.1.9 (192.168.1.9), 30 hops max, 60 byte packets
 1  * * *
 2  * * 192.168.1.9 (192.168.1.9)  0.245 ms

```
