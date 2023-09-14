## ICMP echo request
   - To use ICMP echo request to discover live hosts, add the option `-PE`. (Remember to add `-sn` if you don’t want to follow that with a port scan.)
   - As shown in the following figure, an ICMP echo scan works by sending an ICMP echo request and expects the target to reply with an ICMP echo reply if it is online.

![[nmap12.png]]

**Command** - 
```python
sudo nmap -PE -sn 10.10.68.220/24
```

![[nmap13.png]]
The scan output shows that eight hosts are up; moreover, it shows their MAC addresses. Generally speaking, we don’t expect to learn the MAC addresses of the targets unless they are on the same subnet as our system.

**We will repeat the scan above; however, this time, we will scan from a system that belongs to a different subnet. The results are similar but without the MAC addresses.**
![[nmap14.png]]

**Note** - Because ICMP echo requests tend to be blocked, you might also consider ICMP Timestamp or ICMP Address Mask requests to tell if a system is online.

## ICMP timestamp request
   - Nmap uses timestamp request (ICMP Type 13) and checks whether it will get a Timestamp reply (ICMP Type 14).
   - Adding the `-PP` option tells Nmap to use ICMP timestamp requests.

**As shown in the figure below, you expect live hosts to reply.**
![[nmap15.png]]

**In the following example, we run `nmap -PP -sn MACHINE_IP/24` to discover the online computers on the target machine subnet.**
![[nmap16.png]]
Similar to the previous ICMP scan, this scan will send many ICMP timestamp requests to every valid IP address in the target subnet.

## ICMP address mask request
   - Nmap uses address mask queries (ICMP Type 17) and checks whether it gets an address mask reply (ICMP Type 18).
   - This scan can be enabled with the option `-PM`. As shown in the figure below, live hosts are expected to reply to ICMP address mask requests.
![[nmap17.png]]

**Command** - 
```python
nmap -PM -sn MACHINE_IP/24
```
