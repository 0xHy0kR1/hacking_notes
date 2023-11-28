
## Idle scan
   - The idle scan, or zombie scan, requires an idle system connected to the network that you can communicate with.
   - Practically, Nmap will make each probe appear as if coming from the idle (zombie) host, then it will check for indicators whether the idle (zombie) host received any response to the spoofed probe.
   - This is accomplished by checking the IP identification (IP ID) value in the IP header.

>You can run an idle scan using the below command:
```shell
nmap -sI ZOMBIE_IP MACHINE_IP
```
`ZOMBIE_IP` is the IP address of the idle host (zombie).

**The idle (zombie) scan requires the following three steps to discover whether a port is open:**
1. Trigger the idle host to respond so that you can record the current IP ID on the idle host.
2. Send a SYN packet to a TCP port on the target. The packet should be spoofed to appear as if it was coming from the idle host (zombie) IP address.
3. Trigger the idle machine again to respond so that you can compare the new IP ID with the one received earlier.

**Let’s explain with figures.**
>In the figure below, we have the attacker system probing an idle machine, a multi-function printer. By sending a SYN/ACK, it responds with an RST packet containing its newly incremented IP ID.
![[nmap41.png]]

- The attacker will send a SYN packet to the TCP port they want to check on the target machine in the next step. However, this packet will use the idle host (zombie) IP address as the source.
  **Three scenarios would arise**
  
  >In the first scenario, shown in the figure below, the TCP port is closed; therefore, the target machine responds to the idle host with an RST packet. The idle host does not respond; hence its IP ID is not incremented.
![[nmap42.png]]


> In the second scenario, as shown below, the TCP port is open, so the target machine responds with a SYN/ACK to the idle host (zombie). The idle host responds to this unexpected packet with an RST packet, thus incrementing its IP ID.
![[nmap43.png]]


In the third scenario, the target machine does not respond at all due to firewall rules. This lack of response will lead to the same result as with the closed port; the idle host won’t increase the IP ID.

- For the final step, the attacker sends another SYN/ACK to the idle host. The idle host responds with an RST packet, incrementing the IP ID by one again.
- The attacker needs to compare the IP ID of the RST packet received in the first step with the IP ID of the RST packet received in this third step.
- If the difference is 1, it means the port on the target machine was closed or filtered. However, if the difference is 2, it means that the port on the target was open.
- In this console output above, we can see that this system is considered online because Nmap “received arp-response.”
- On the other hand, we know that the SSH port is deemed to be open because Nmap received a “syn-ack” packet back.
## Some extra points
   - You might consider adding `--reason` if you want Nmap to provide more details regarding its reasoning and conclusions.
     
     **Consider  the two scans**
     ![[nmap44.png]]
     
     ![[nmap45.png]]
     Providing the `--reason` flag gives us the explicit reason why Nmap concluded that the system is up or a particular port is open.
     
     - For more detailed output, you can consider using `-v` for verbose output or `-vv` for even more verbosity.
     - If `-vv` does not satisfy your curiosity, you can use `-d` for debugging details or `-dd` for even more details.