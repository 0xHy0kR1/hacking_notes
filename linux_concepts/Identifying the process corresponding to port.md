- there are several ways to identify the process that is using a specific port.
## Using the `fuser` command on linux
```python
┌──(hyok㉿kali)-[~]
└─$ netstat -tuln                      
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 127.0.0.1:5432          0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:1234            0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:8834            0.0.0.0:*               LISTEN     
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN     
tcp6       0      0 :::22                   :::*                    LISTEN     
tcp6       0      0 :::8834                 :::*                    LISTEN     
tcp6       0      0 ::1:5432                :::*                    LISTEN     
udp        0      0 224.0.0.251:5353        0.0.0.0:*                          
udp6       0      0 fe80::a00:27ff:fedf:546 :::*                 
```
- Now, finding the process among them.
```python
┌──(hyok㉿kali)-[~]
└─$ sudo fuser -n tcp 1234

[sudo] password for hyok: 
1234/tcp:             6021
```
