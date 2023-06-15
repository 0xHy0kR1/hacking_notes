- The ping command is used when we want to test whether a connection to a remote resource is possible.
- Ping works using the ICMP protocol.
- The ICMP protocol works on the Network layer of the OSI Model, and thus the Internet layer of the TCP/IP model.

## Syntax
```bash
ping <target>
```

## Example
```bash
┌──(hyok㉿kali)-[~/Downloads]
└─$ ping muirlandoracle.co.uk
PING muirlandoracle.co.uk (217.160.0.152) 56(84) bytes of data.
64 bytes from 217-160-0-152.elastic-ssl.ui-r.com (217.160.0.152): icmp_seq=1 ttl=54 time=157 ms
64 bytes from 217-160-0-152.elastic-ssl.ui-r.com (217.160.0.152): icmp_seq=2 ttl=54 time=206 ms
^C
--- muirlandoracle.co.uk ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1000ms
rtt min/avg/max/mdev = 157.082/181.749/206.417/24.667 ms
```

- it can be used to determine the IP address of the server hosting a website.