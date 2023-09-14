## Introduction
- The primary purpose of ping is to check whether you can reach the remote system and that the remote system can reach you back.
- In other words, initially, this was used to check network connectivity; however, we are more interested in its different uses: checking whether the remote system is online.
- In simple terms, the ping command sends a packet to a remote system, and the remote system replies. This way, you can conclude that the remote system is online and that the network is working between the two systems.
- the ping is a command that sends an ICMP Echo packet to a remote system. If the remote system is online, and the ping packet was correctly routed and not blocked by any firewall, the remote system should send back an ICMP Echo Reply. Similarly, the ping reply should reach the first system if appropriately routed and not blocked by any firewall.

### Syntax - 
```shell
ping 10.10.183.50
```
OR
```shell
ping HOSTNAME
```
- In the latter, the system needs to resolve HOSTNAME to an IP address before sending the ping packet.
- If you don’t specify the count on a Linux system, you will need to hit `CTRL+c` to force it to stop.

**Hence, you might consider below command to send ten packets:**
**Linux** - 
```shell
ping -c 10 10.10.183.50
```

**Windows** - 
```shell
ping -n 10 10.10.183.50
```

![[active_recon1.png]]
- In the example above, we saw clearly that the target system is responding. The ping output is an indicator that it is online and reachable. 
- We notice that, on average, it took 0.475 ms (millisecond) for the reply to reach our system, with the maximum being 0.636 ms.

**Let’s consider the following case: we shut down the target virtual machine and then tried to ping `10.10.183.50`.**
![[active_recon2.png]]
As you would expect in the following example, we don’t receive any reply.

**Generally speaking, when we don’t get a ping reply back, there are a few explanations that would explain why we didn’t get a ping reply, for example:**
- The destination computer is not responsive; possibly still booting up or turned off, or the OS has crashed.
- It is unplugged from the network, or there is a faulty network device across the path.
- A firewall is configured to block such packets. The firewall might be a piece of software running on the system itself or a separate network appliance. Note that MS Windows firewall blocks ping by default.
- Your system is unplugged from the network.
