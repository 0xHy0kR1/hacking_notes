## Introduction
- the traceroute command _traces the route_ taken by the packets from your system to another host.
- The purpose of a traceroute is to find the IP addresses of the routers or hops that a packet traverses as it goes from your system to a target host.
- This command also reveals the number of routers between the two systems.
- It is helpful as it indicates the number of hops (routers) between your system and the target host. However, note that the route taken by the packets might change as many routers use dynamic routing protocols that adapt to network changes.
- On Linux, `traceroute` will start by sending UDP datagrams within IP packets of TTL being 1. Thus, it causes the first router to encounter a TTL=0 and send an ICMP Time-to-Live exceeded back. Hence, a TTL of 1 will reveal the IP address of the first router to you.

### Syntax - 
```shell
traceroute MACHINE_IP
```

- TTL indicates the maximum number of routers/hops that a packet can pass through before being dropped. When a router receives a packet, it decrements the TTL by one before passing it to the next router.
- The following figure shows that each time the IP packet passes through a router, its TTL value is decremented by 1.
![[traceroute1.png]]
However, if the TTL reaches 0, it will be dropped, and an ICMP Time-to-Live exceeded would be sent to the original sender.

**The first router on the path decrements the TTL by 1, resulting in a TTL of 0. Consequently, this router will discard the packet and send an ICMP time exceeded in-transit error message. Note that some routers are configured not to send such ICMP messages when discarding a packet.**
![[traceroute2.png]]

- On Linux, `traceroute` will start by sending UDP datagrams within IP packets of TTL being 1. Thus, it causes the first router to encounter a TTL=0 and send an ICMP Time-to-Live exceeded back. Hence, a TTL of 1 will reveal the IP address of the first router to you.

- Then it will send another packet with TTL=2; this packet will be dropped at the second router. And so on.

### Example - 1
![[active_recon3.png]]
- In the traceroute output above, we have 14 numbered lines; each line represents one router/hop.
- Our system sends three packets with TTL set to 1, then three packets with TTL set to 2, and so forth.
- On the other hand, we can see that we received only a single reply on the third line. The two stars in the output `3 * 100.66.16.176 (100.66.16.176) 8.006 ms *` indicate that our system didn’t receive two expected ICMP time exceeded in-transit messages.
- Consider line number 12, the twelfth router with the listed IP address has dropped the packet three times and sent an ICMP time exceeded in-transit message. The line `12 99.83.69.207 (99.83.69.207) 17.603 ms 15.827 ms 17.351 ms` shows the time in milliseconds for each reply to reach our system.
- Finally, in the first line of the output, we can see that the packets leaving the AttackBox take different routes. We can see two routers that responded to TTL being one. Our system never received the third expected ICMP message.

### Example - 1
![[active_recon4.png]]
- In the second run of the traceroute program, we noticed that the packets took a longer route this time, passing through 26 routers. If you are running a traceroute to a system within your network, the route will be unlikely to change.

**To summarize, we can notice the following:**
   - The number of hops/routers between your system and the target system depends on the time you are running traceroute. There is no guarantee that your packets will always follow the same route, even if you are on the same network or you repeat the traceroute command within a short time.
   - Some routers return a public IP address. You might examine a few of these routers based on the scope of the intended penetration testing.
   - Some routers don’t return a reply.

