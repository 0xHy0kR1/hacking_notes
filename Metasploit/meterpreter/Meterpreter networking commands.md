- Pivoting is a concept by which we can compromise other machines on the same network in which our target is present.
## There are several networking commands provided by Meterpreter, which we can display using the help command followed by net for the network:
```python
meterpreter > help net

Stdapi: Networking Commands
===========================

    Command       Description
    -------       -----------
    arp           Display the host ARP cache
    getproxy      Display the current proxy configuration
    ifconfig      Display interfaces
    ipconfig      Display interfaces
    netstat       Display the network connections
    portfwd       Forward a local port to a remote service
    resolve       Resolve a set of host names on the target
    route         View and modify the routing table
```

## The arp command displays the host ARP cache:
```python
meterpreter > arp

ARP cache
=========

    IP address       MAC address        Interface
    ----------       -----------        ---------
    192.168.216.1    52:54:00:12:35:00  11
    192.168.216.3    08:00:27:02:be:15  11
    192.168.216.9    08:00:27:df:52:8a  11
    192.168.216.255  ff:ff:ff:ff:ff:ff  11
    224.0.0.22       00:00:00:00:00:00  1
    224.0.0.22       01:00:5e:00:00:16  11
    224.0.0.251      01:00:5e:00:00:fb  11
    224.0.0.252      01:00:5e:00:00:fc  11
    224.2.2.4        01:00:5e:02:02:04  11
    239.77.124.213   00:00:00:00:00:00  1
    239.77.124.213   01:00:5e:4d:7c:d5  11
    255.255.255.255  ff:ff:ff:ff:ff:ff  11
```

## getproxy command allows us to see the current proxy configuration:
```python
meterpreter > getproxy
Auto-detect     : Yes
Auto config URL : 
Proxy URL       : 
Proxy Bypass    : 
```

## The ipconfig/ifconfig commands are used to display all the TCP/IP network configurations of the target machine:
```python
meterpreter > ifconfig

Interface  1
============
Name         : Software Loopback Interface 1
Hardware MAC : 00:00:00:00:00:00
MTU          : 4294967295
IPv4 Address : 127.0.0.1
IPv4 Netmask : 255.0.0.0
IPv6 Address : ::1
IPv6 Netmask : ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff


Interface 11
============
Name         : Intel(R) PRO/1000 MT Desktop Adapter
Hardware MAC : 08:00:27:41:0f:1c
MTU          : 1500
IPv4 Address : 192.168.216.11
IPv4 Netmask : 255.255.255.0
IPv6 Address : fe80::c1c4:7743:15f5:1e11
IPv6 Netmask : ffff:ffff:ffff:ffff::


Interface 12
============
Name         : Microsoft ISATAP Adapter
Hardware MAC : 00:00:00:00:00:00
MTU          : 1280
IPv6 Address : fe80::5efe:c0a8:d80b
IPv6 Netmask : ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff
```

## The netstat command displays the network connections:
```python
meterpreter > netstat

Connection list
===============

    Proto  Local address         Remote address        State        User  Inode  PID/Program name
    -----  -------------         --------------        -----        ----  -----  ----------------
    tcp    0.0.0.0:21            0.0.0.0:*             LISTEN       0     0      1512/svchost.exe
    tcp    0.0.0.0:22            0.0.0.0:*             LISTEN       0     0      2236/sshd.exe
    tcp    0.0.0.0:80            0.0.0.0:*             LISTEN       0     0      4/System
    tcp    0.0.0.0:135           0.0.0.0:*             LISTEN       0     0      712/svchost.exe
    tcp    0.0.0.0:445           0.0.0.0:*             LISTEN       0     0      4/System
-----------------------------------------SNIP----------------------------------
```

## Displaying network routes with "route" command:
```python
meterpreter > route

IPv4 network routes
===================

    Subnet           Netmask          Gateway         Metric  Interface
    ------           -------          -------         ------  ---------
    0.0.0.0          0.0.0.0          192.168.216.1   10      11
    127.0.0.0        255.0.0.0        127.0.0.1       306     1
    127.0.0.1        255.255.255.255  127.0.0.1       306     1
    127.255.255.255  255.255.255.255  127.0.0.1       306     1
    192.168.216.0    255.255.255.0    192.168.216.11  266     11
    192.168.216.11   255.255.255.255  192.168.216.11  266     11
    192.168.216.255  255.255.255.255  192.168.216.11  266     11
    224.0.0.0        240.0.0.0        127.0.0.1       306     1
    224.0.0.0        240.0.0.0        192.168.216.11  266     11
    255.255.255.255  255.255.255.255  127.0.0.1       306     1
    255.255.255.255  255.255.255.255  192.168.216.11  266     11

No IPv6 routes were found.
```
- The "route" command in Meterpreter is used to manage the routing table of the compromised system. 
- A routing table is a database that contains information about the available network routes that a computer can use to send and receive data.

## port forwarding with a remote host
```python
meterpreter> portfwd -a -L 127.0.0.1 -l 444 -h 69.54.34.38 -p 3389
```

### Pre-requisite --> [[port forwarding]]
#### Explaination to above command 
So imagine you have two computers, A and B. Computer A wants to talk to computer B, but they are not directly connected. To make them talk, we can create a special "tunnel" between them, called a port forwarding connection. 

Here's what each part of the command means:
- "meterpreter >" is just the prompt where the command is typed.
- "portfwd" is the name of the command that creates the tunnel.
- "-a" means to add a new port forwarding rule.
- "-L 127.0.0.1" means to listen on the local computer(computer A) on the IP address 127.0.0.1.
- "-l 444" means to listen on port 444 on the local computer(computer A).
- The "-h" flag stands for "host", and it specifies the IP address of the remote computer that you want to connect to. In this case, that IP address is 69.54.34.38. So when you run this command, it sets up a connection that forwards traffic to the specified IP address (computer B). This allows computer A to communicate with computer B, even if they are not directly connected to each other.
- "-h 69.54.34.38"  means to forward the connection to the remote comuter(computer B) at Ip address 69.54.34.38.
- "-p 3389" means to forward the connection to port 3389 on the remote computer(computer B).