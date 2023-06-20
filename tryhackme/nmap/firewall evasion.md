## nmap towards windows firewall:
Windows host will, with its default firewall, block all ICMP packets. This means that Nmap will register a host with this firewall configuration as dead and not bother scanning it at all.
## Some nmap switches:
1. `-Pn`
	- It tells Nmap to not bother pinging the host before scanning it. This means that Nmap will always treat the target host(s) as being alive, effectively bypassing the ICMP block
	- It potentially taking a very long time to complete the scan (if the host really is dead then Nmap will still be checking and double checking every specified port).

2. `-f`
	- Used to fragment the packets (i.e. split them into smaller pieces) making it less likely that the packets will be detected by a firewall or IDS.

3. `--mtu <number>`
	- accepts a maximum transmission unit size to use for the packets sent. This _must_ be a multiple of 8.
	- It an alternative to `-f`

4. `--scan-delay <time>ms`
	- It is used to add a delay between packets sent.
	- This is very useful if the network is unstable, but also for evading any time-based firewall/IDS triggers which may be in place.

5. `--badsum`
	- this is used to generate in invalid checksum for packets.
	- Any real TCP/IP stack would drop this packet, however, firewalls may potentially respond automatically, without bothering to check the checksum of the packet.
	- this switch can be used to determine the presence of a firewall/IDS.