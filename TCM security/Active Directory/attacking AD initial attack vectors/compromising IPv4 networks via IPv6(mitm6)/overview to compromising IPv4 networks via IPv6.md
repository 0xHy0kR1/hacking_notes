## Introduction
- An attack is presented that abuses the default IPv6 configuration in Windows networks to spoof DNS replies by acting as a malicious DNS server and redirect traffic to an attacker specified endpoint.
- In the second phase of this attack, a new method is outlined to exploit the (infamous) Windows Proxy Auto Discovery (WPAD) feature in order to relay credentials and authenticate to various services within the network.

## IPv6 attacks
- mitm6 is a tool which focusses on an easy to setup solution that selectively attacks hosts and spoofs DNS replies, while minimizing the impact on the network’s regular operation.
- When the attack is stopped, the network reverts itself to it’s previous state within minutes due to the tweaked timeouts set in the tool.

![[compromise_ipv4_via_ipv6_3.png]]