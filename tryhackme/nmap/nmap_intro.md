Nmap was created by Gordon Lyon (Fyodor), a network security expert and open source programmer. It was released in 1997. Nmap, short for Network Mapper, is free, open-source software released under GPL license.

**A Nmap scan usually goes through the steps shown in the figure below, although many are optional and depend on the command-line arguments you provide.**
![[nmap10.png]]


## nmap scan 
This option will provide you with a **complete list of the hosts** that Nmap will scan without actually scanning them; however, Nmap will perform reverse-DNS resolution on all targets to retrieve their names.
```python
nmap -n -sL 10.10.12.13/29
```
If you don’t want Nmap to the DNS server, you can add `-n`

## Nmap host discovery ARP

**When no host discovery options are provided, Nmap follows the following approaches to discover live hosts:**
1. When a _privileged_ user tries to scan targets on a local network (Ethernet), Nmap uses _ARP requests_. A privileged user is `root` or a user who belongs to `sudoers` and can run `sudo`.
2. When a _privileged_ user tries to scan targets outside the local network, Nmap uses ICMP echo requests, TCP ACK (Acknowledge) to port 80, TCP SYN (Synchronize) to port 443, and ICMP timestamp request.
3. When an _unprivileged_ user tries to scan targets outside the local network, Nmap resorts to a TCP 3-way handshake by sending SYN packets to ports 80 and 443.

Nmap, by default, uses a ping scan to find live hosts, then proceeds to scan live hosts only.

###### To discover online hosts without port-scanning the live systems, you can use the below command: 
```python
nmap -sn TARGETS
```

##### If you want Nmap only to perform an ARP scan without port-scanning, you can use the below command:
```python
nmap -PR -sn TARGETS
```
where `-PR` indicates that you only want an ARP scan.
we are requesting the MAC addresses of all the IP addresses on the subnet, starting with `10.10.210.1`.
![[nmap11.png]]

##### send ARP queries to all valid IP addresses on your local networks
```python
arp-scan --localnet
```
OR
```python
arp-scan -l
```

##### Specifying the interface to scan
```python
sudo arp-scan -I eth0 -l
```
It will send ARP queries for all valid IP addresses on the `eth0` interface.

### Nmap considers the following six states:

1. **Open:**
	- indicates that a service is listening on the specified port.

2. **Closed:**
	- indicates that no service is listening on the specified port, although the port is accessible. By accessible, we mean that it is reachable and is not blocked by a firewall or other security appliances/programs.

3. **Filtered:**
	- means that Nmap cannot determine if the port is open or closed because the port is not accessible.
	- This state is usually due to a firewall preventing Nmap from reaching that port. Nmap’s packets may be blocked from reaching the port; alternatively, the responses are blocked from reaching Nmap’s host.

4. **Unfiltered**:
	- means that Nmap cannot determine if the port is open or closed, although the port is accessible.
	- This state is encountered when using an ACK scan `-sA`.

5. **Open|Filtered**:
	- This means that Nmap cannot determine whether the port is open or filtered.

6. **Closed|Filtered:**
	- This means that Nmap cannot decide whether a port is closed or filtered.

