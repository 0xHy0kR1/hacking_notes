Nmap was created by Gordon Lyon (Fyodor), a network security expert and open source programmer. It was released in 1997. Nmap, short for Network Mapper, is free, open-source software released under GPL license.

**A Nmap scan usually goes through the steps shown in the figure below, although many are optional and depend on the command-line arguments you provide.**
![[nmap10.png]]


## nmap scan 
This option will provide you with a **complete list of the hosts** that Nmap will scan without actually scanning them; however, Nmap will perform reverse-DNS resolution on all targets to retrieve their names.
```python
nmap -n -sL 10.10.12.13/29
```
`-n`: This option tells Nmap not to perform DNS resolution. In other words, it will not attempt to resolve IP addresses to hostnames. This can make the scan faster because it doesn't have to wait for DNS queries to complete.

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

**Note** - 
1. we can use `-F` to enable fast mode and decrease the number of scanned ports from 1000 to 100 most common ports.
2. the `-r` option can also be added to scan the ports in consecutive order instead of random order.
3. You can control the scan timing using `-T<0-5>`. `-T0` is the slowest (paranoid), while `-T5` is the fastest.
4. To avoid IDS alerts, you might consider `-T0` or `-T1`.
5. You expect to specify the network interface using `-e` and to explicitly disable ping scan `-Pn`.

## Some extra information about nmap

1. **According to Nmap manual page, there are six templates:**
- paranoid (0)
- sneaky (1)
- polite (2)
- normal (3)
- aggressive (4)
- insane (5)

2. `-T0` scans one port at a time and waits 5 minutes between sending each probe, so you can guess how long scanning one target would take to finish.
3. If you don’t specify any timing, Nmap uses normal `-T3`. Note that `-T5` is the most aggressive in terms of speed; however, this can affect the accuracy of the scan results due to the increased likelihood of packet loss.
4. Note that `-T4` is often used during CTFs and when learning to scan on practice targets
5. `-T1` is often used during real engagements where stealth is more important.
6. Alternatively, you can choose to control the packet rate using `--min-rate <number>` and `--max-rate <number>`.
For example, `--max-rate 10` or `--max-rate=10` ensures that your scanner is not sending more than ten packets per second.

7. Moreover, you can control probing parallelization using `--min-parallelism <numprobes>` and `--max-parallelism <numprobes>`
	probing parallelization specifies the number of such probes that can be run in parallel. For instance, `--min-parallelism=512` pushes Nmap to maintain at least 512 probes in parallel; these 512 probes are related to host discovery and open ports.


#### TCP ACK Scan
   - As the name implies, an ACK scan will send a TCP packet with the ACK flag set.
   - Use the `-sA` option to choose this scan.
   - This scan won’t tell us whether the target port is open in a simple setup.
   - based on which ACK packets resulted in responses, you will learn which ports were not blocked by the firewall. In other words, this type of scan is more suitable to discover firewall rule sets and configuration.

![[nmap32.png]]

> Syntax
```shell
sudo nmap -sA 10.10.148.92
```

![[nmap33.png]]
As seen in the console output above, we have three ports that aren't being blocked by the firewall. This result indicates that the firewall is blocking all other ports except for these three ports.

#### Window Scan
   - Another similar scan is the TCP window scan. The TCP window scan is almost the same as the ACK scan; however, it examines the TCP Window field of the RST packets returned.
   - On specific systems, this can reveal that the port is open.
   - You can select this scan type with the option `-sW`.
   - As shown in the figure below, we expect to get an RST packet in reply to our “uninvited” ACK packets, regardless of whether the port is open or closed.
   - Similarly, launching a TCP window scan against a Linux system with no firewall will not provide much information.
![[nmap34.png]]

As we can see in the console output below, the results of the window scan against a Linux server with no firewall didn’t give any extra information compared to the ACK scan executed earlier.
![[nmap35.png]]

However, as you would expect, if we repeat our TCP window scan against a server behind a firewall, we expect to get more satisfying results. In the console output shown below
![[nmap36.png]]

#### Custom Scan
   - If you want to experiment with a new TCP flag combination beyond the built-in TCP scan types, you can do so using `--scanflags`.
   - For instance, if you want to set SYN, RST, and FIN simultaneously, you can do so using `--scanflags RSTSYNFIN`. As shown in the figure below.
   - If you develop your custom scan, you need to know how the different ports will behave to interpret the results in different scenarios correctly.
![[nmap37.png]]

**Note** - 
1. Finally, it is essential to note that the ACK scan and the window scan were very efficient at helping us map out the firewall rules.
2. However, it is vital to remember that just because a firewall is not blocking a specific port, it does not necessarily mean that a service is listening on that port.
3. ACK and window scans are exposing the firewall rules, not the services.

## Spoofing IP with nmap
   - If you try to scan a target from some random network using a spoofed IP address, chances are you won’t have any response routed to you, and the scan results could be unreliable.
   - The following figure shows the attacker launching the command `nmap -S SPOOFED_IP 10.10.245.208`. Consequently, Nmap will craft all the packets using the provided source IP address `SPOOFED_IP`.
   - The target machine will respond to the incoming packets sending the replies to the destination IP address `SPOOFED_IP`.
   - For this scan to work and give accurate results, the attacker needs to monitor the network traffic to analyze the replies.
![[nmap38.png]]

##### scanning with a spoofed IP address is three steps:

   1. Attacker sends a packet with a spoofed source IP address to the target machine.
   2. Target machine replies to the spoofed IP address as the destination.
   3. Attacker captures the replies to figure out open ports.

>Scanning with spoofed ip and perticular interface
```shell
nmap -e NET_INTERFACE -Pn -S SPOOFED_IP 10.10.245.208
```
- When you are on the same subnet as the target machine, you would be able to spoof your MAC address as well. You can specify the source MAC address using `--spoof-mac SPOOFED_MAC`.
- This address spoofing is only possible if the attacker and the target machine are on the same Ethernet (802.3) network or same WiFi (802.11).

## Decoying IP
   - The concept is simple, make the scan appear to be coming from many IP addresses so that the attacker’s IP address would be lost among them.
   - As we see in the figure below, the scan of the target machine will appear to be coming from 3 different sources, and consequently, the replies will go the decoys as well.
![[nmap39.png]]


>Decoy scan by specifying a specific or random IP address
```shell
nmap -D 10.10.0.1,10.10.0.2,ME MACHINE_IP
```
the scan of 10.10.24.80 appear as coming from the IP addresses 10.10.0.1, 10.10.0.2, and then `ME` to indicate that your IP address should appear in the third order.


>Decoy scan by specifying a specific and as well as random ip addresses
```shell
nmap -D 10.10.0.1,10.10.0.2,RND,RND,ME 10.10.24.80
```
where the third and fourth source IP addresses are assigned randomly, while the fifth source is going to be the attacker’s IP address.

### Firewall
   - A firewall is a piece of software or hardware that permits packets to pass through or blocks them.
   - A traditional firewall inspects, at least, the IP header and the transport layer header.
   - A more sophisticated firewall would also try to examine the data carried by the transport layer.

### IDS
   - An intrusion detection system (IDS) inspects network packets for select behavioural patterns or specific content signatures. It raises an alert whenever a malicious rule is met.
   - An IDS would inspect the data contents in the transport layer and check if it matches any malicious patterns.

### Fragmented Packets
   - Nmap provides the option `-f` to fragment packets.
   - Adding another `-f` (`-f -f` or `-ff`) will split the data into 16 byte-fragments instead of 8.
   - You can change the default value by using the `--mtu`; however, you should always choose a multiple of 8.
   - if you prefer to increase the size of your packets to make them look innocuous, you can use the option `--data-length NUM`, where num specifies the number of bytes you want to append to your packets.
   
#####  Comparing fragmentation vs non framentation
   Let’s compare running `sudo nmap -sS -p80 10.20.30.144` and `sudo nmap -sS -p80 -f 10.20.30.144`.

   in the second command, we are requesting Nmap to fragment the IP packets.
   
   **Analysis of `sudo nmap -sS -p80 10.20.30.144` via wireshark**
   ![[nmap40.png]]
   - In the first two lines, we can see an ARP query and response. Nmap issued an ARP query because the target is on the same Ethernet.
   - The second two lines show a TCP SYN ping and a reply.
   - The fifth line is the beginning of the port scan; Nmap sends a TCP SYN packet to port 80. In this case, the IP header is 20 bytes, and the TCP header is 24 bytes.
   - Note that the minimum size of the TCP header is 20 bytes.
     
 **Analysis of `sudo nmap -sS -p80 -f 10.20.30.144` via wireshark**
   - With fragmentation requested via `-f`, the 24 bytes of the TCP header will be divided into multiples of 8 bytes, with the last fragment containing 8 bytes or less of the TCP header.
   - Since 24 is divisible by 8, we got 3 IP fragments; each has 20 bytes of IP header and 8 bytes of TCP header.



   