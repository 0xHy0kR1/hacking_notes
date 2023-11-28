Consider a user checking his email messages using POP3.
>Capturing username and password using tcpdump
```sh
sudo tcpdump port 110 -A
```
- This attack requires access to the network traffic, for example, via a wiretap or a switch with port mirroring. 
- Alternatively, we can access the traffic exchanged if we launch a successful Man-in-the-Middle (MITM) attack.
- We need `sudo` as packet captures require root privileges.
- We know that POP3 uses port 110, so we filtered our packets using `port 110`.
- Finally, we wanted to display the contents of the captured packets in ASCII format, so we added `-A`.

![[sniffinga1.png]]
![[sniffinga2.png]]
In brief, any protocol that uses cleartext communication is susceptible to this kind of attack.

### Man-in-the-Middle (MITM)
   We have A requesting the transfer of $20 to M; however, E altered this message and replaced the original value with a new one. B received the modified messaged and acted on it.
   ![[sniffinga3.png]]
- Any time you browse over HTTP, you are susceptible to a MITM attack, and the scary thing is that you cannot recognize it
- Many tools would aid you in carrying out such an attack, such as [Ettercap](https://www.ettercap-project.org/) and [Bettercap](https://www.bettercap.org/).
- MITM can also affect other cleartext protocols such as FTP, SMTP, and POP3. 