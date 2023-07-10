## The mitm6 attack
- mitm6 starts with listening on the primary interface of the attacker machine for Windows clients requesting an IPv6 configuration via DHCPv6.
- mitm6 will reply to those DHCPv6 requests, assigning the victim an IPv6 address within the link-local range. While in an actual IPv6 network these addresses are auto-assigned by the hosts themselves and do not need to be configured by a DHCP server, this gives us the opportunity to set the attackers IP as the default IPv6 DNS server for the victims.
- mitm6 does not advertise itself as a gateway, and thus hosts will not actually attempt to communicate with IPv6 hosts outside their local network segment or VLAN.
- Optionally it will periodically send Router Advertisment (RA) messages to alert client that there is an IPv6 network in place and that clients should request an IPv6 adddress via DHCPv6.
- This will in some cases speed up the attack but is not required for the attack to work, making it possible to execute this attack on networks that have protection against the SLAAC attack with features such as [RA Guard](https://www.juniper.net/documentation/en_US/junos/topics/concept/port-security-ra-guard.html).

**Primary DNS takeover done through below command as follows:**
```python
sudo mitm6 -d MARVEL.local
```

**Note** - It should be noted that mitm6 currently only targets Windows based operating systems, since other operating systems like macOS and Linux do not use DHCPv6 for DNS server assignment.

