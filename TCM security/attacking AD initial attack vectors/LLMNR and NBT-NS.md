[Top_five_ways_to_get_domain](https://medium.com/@adam.toscher/top-five-ways-i-got-domain-admin-on-your-internal-network-before-lunch-2018-edition-82259ab73aaa)
## What is LLMNR (link-local multicast Name resolution) and NBT-NS
- Link-Local Multicast Name Resolution (**LLMNR**) and NetBIOS Name Service (**NBT-NS)** are two name services used by windows for resolving hostnames to IP addresses when a DNS request fails in a network.
- In a network, if a machine tries to resolve a particular host and DNS fails to do so, the machine will communicate with other machines in the network using the LLMNR and ask if anyone knows the particular hosts.

## LLMNR poisoning
- In Active Directory environments, we often see that LLMNR is enabled and it is used widely.
- But using the LLMNR host resolution has a severe security impact, as when a non-existing host is searched using the **LLMNR** method. it broadcasts the request to every system that is connected to the local network. and if we have any compromised machine on the local network by default it will also receive the host query request and the compromised machine can also send the response to the victim machine. and in turn, ask for the password hash of the victim.

## Working of LLMR poisoning:
![[AD_in1.png]]

1. the victim machine wants to connect **_\\sharefiles_**, but mistakenly typed in **_\\shrefiles_**
2. The DNS server responds to the victim **_\\shrefiles_** — **NOT FOUND**
3. then the victim sends out a Broadcast asking if anyone on the local network knows the location of **_\\shrefiles_**
4. The attacker machine pretends to be "\shrefiles" and responds to the victim, saying, "Yes, I am \shrefiles." The attacker's goal is to trick the victim into connecting to it.
5. When the victim machine tries to connect to "\shrefiles", it sends its username and a cryptographic password hash called NTLMv2 Hash to the attacker machine, thinking it is connecting to the correct shared folder.
6. However, the attacker machine is not really "\shrefiles" and doesn't have the actual shared folder. So, it sends an error message back to the victim machine, indicating that there was a problem and the connection couldn't be established.

In summary, the attacker tricks the victim into connecting to a fake shared folder by responding to the victim's broadcast message. The attacker then captures the victim's username and password hash and sends an error message, preventing the victim from connecting to the actual shared folder.

## Steps to perform LLMNR poisoning practically:
![[AD_in2.png]]
![[AD_in_LLMNR1.png]]
![[AD_in_LLMNR2.png]]
![[AD_in_LLMNR3.png]]

## Below performing on lab:
1. Starting the responder:
![[AD_in_LLMNR_prac2.png]]

2. Client tries to connect to attack SMB server:
![[AD_in_LLMNR_prac1.png]]

3. Attacker gains the hash of password and username of client:
![[AD_in_LLMNR_prac3.png]]

4. Cracking this hash with hashcat:
**Running in kali linux**
```python
┌──(hyok㉿kali)-[~]
└─$ hashcat -m 5600 ntlmhash.txt /usr/share/wordlists/rockyou.txt --force
```
`--force` --> to force the hashcat to use gpu of base system
`-m 5600` --> to tell the hashcat to use **ntlmv2** method.
`/usr/share/wordlists/rockyou.txt` --> path to wordlists
`ntlmhash.txt` --> hash of step 3 
**plaintext of hash**
![[AD_in_LLMNR_prac4_1.png]]

**Running in windows and it is recommended to run in windows(base system to utilize gpu ruther than cpu)**
![[AD_in_LLMNR_prac_4_2.png]]

## LLMNR Defense:
![[AD_in_LLMNR_defense1.png]]