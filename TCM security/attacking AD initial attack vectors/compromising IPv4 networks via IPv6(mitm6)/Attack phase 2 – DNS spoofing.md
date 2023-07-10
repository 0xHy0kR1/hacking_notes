


## Introduction
- the IPv6 DNS server will be preferred to the IPv4 DNS server. The IPv6 DNS server will be used to query both for A (IPv4) and AAAA (IPv6) records.
- Now our next step is to get clients to connect to the attacker machine instead of the legitimate servers. Our end goal is getting the user or browser to automatically authenticate to the attacker machine, which is why we are spoofing URLs in the internal domain `testsegment.local`

## Exploiting WPAD
**WPAD** - 
Its legitimate use is to automatically detect a network proxy used for connecting to the internet in corporate environments.
The Windows Proxy Auto Detection feature has been a much debated one, and one that has been abused by penetration testers for years

- the address of the server providing the wpad.dat file (which provides this information) would be resolved using DNS, and if no entry was returned, the address would be resolved via insecure broadcast protocols such as Link-Local Multicast Name Resolution (LLMNR).
- An attacker could reply to these broadcast name resolution protocols, pretend the WPAD file was located on the attackers server, and then prompt for authentication to access the WPAD file.
- This authentication was provided by default by Windows without requiring user interaction. This could provide the attacker with NTLM credentials from the user logged in on that computer, which could be used to authenticate to services in a process called NTLM relaying.

**two important protections:**
- The location of the WPAD file is no longer requested via broadcast protocols, but only via DNS.  
- Authentication does not occur automatically anymore even if this is requested by the server.

### Exploiting WPAD post [MS16-077](https://support.microsoft.com/en-us/topic/ms16-077-security-update-for-wpad-june-14-2016-2490f086-dc17-4a6e-2799-a974d1af385e)
- The first protection, where WPAD is only requested via DNS, can be easily bypassed with mitm6.
- As soon as the victim machine has set the attacker as IPv6 DNS server, it will start querying for the WPAD configuration of the network.
- Since these DNS queries are sent to the attacker, it can just reply with its own IP address (either IPv4 or IPv6 depending on what the victim’s machine asks for).
- This also works if the organization is already using a WPAD file (though in this case it will break any connections from reaching the internet).
- To bypass the second protection, where credentials are no longer provided by default, we need to do a little more work. When the victim requests a WPAD file we won’t request authentication, but instead provide it with a valid WPAD file where the attacker’s machine is set as a proxy.
- When the victim now runs any application that uses the Windows API to connect to the internet or simply starts browsing the web, it will use the attackers machine as a proxy

Windows will now happily send the NTLM challenge/response to the attacker, who can relay it to different services. With this relaying attack, the attacker can authenticate as the victim on services, access information on websites and shares, and if the victim has enough privileges, the attacker can even execute code on computers or even take over the entire Windows Domain.

**Relaying captured credentials can be done through below commands as follows**
```python
ntlmrelayx.py -6 -t ldaps://192.168.1.15 -wh fakewpad.marvel.local -l lootme
```

## Full attack
- First we start mitm6, which will start replying to DHCPv6 requests and afterwards to DNS queries requesting names in the internal network.
- For the second part of our attack, we use our favorite relaying tool, [ntlmrelayx](https://github.com/CoreSecurity/impacket/blob/master/examples/ntlmrelayx.py)
- improving ntlmrelayx, adding several new features which (among others) enable it to relay via IPv6, serve the WPAD file, automatically detect proxy requests and prompt the victim for the correct authentication.
- To serve the WPAD file, add `-wh` parameter and with it specify the host that the WPAD file resides on.
- To make sure ntlmrelayx listens on both IPv4 and IPv6, use the `-6` parameter.
- mitm6 selectively spoofing DNS replies and ntlmrelayx serving the WPAD file and then relaying authentication to other servers in the network.
![[compromise_ipv4_via_ipv6_1.png]]
**In another tab run the below command**:
![[compromise_ipv4_via_ipv6_2.png]]

## Looking at the lootme folder for the info of domain controller:
![[compromise_ipv4_via_ipv6_4.png]]

## Creating new user inside domain controller:
When the admin of domain controller loged in inside of any other local computer in the network then you can get access to domain and you can create new users inside domain controller
![[compromise_ipv4_via_ipv6_5.png]]


**For extra information related to mitm6** --> https://dirkjanm.io/worst-of-both-worlds-ntlm-relaying-and-kerberos-delegation/