1. A Record
	- This record links a domain name to an IP address
	- It tells your computer which IP address corresponds to the domain name you're trying to reach. It's like looking up a name and finding the associated phone number.

2. AAAA Record (IPv6 Address Record)
	- Similar to the A record, but it maps a domain name to an IPv6 address.
	- It is used for IPv6-enabled networks.

3. CNAME Record
	- It points a domain name to another domain name.
	- It's useful when you want multiple domain names to point to the same IP address. It's like saying, "If you can't find this person, try calling this other person instead."

4. MX Record
	- This record handles email routing.
	- It specifies the mail server responsible for accepting incoming emails for a domain.

5. TXT Record
	- This record allows you to add text information to a domain name.
	- It can be used for various purposes like domain verification, etc.

6. Name server(NS) Record
	- NS records identify the [[Authoritative DNS server]] for a domain.
	- They specify which DNS servers are responsible for resolving and providing information about the domain.

7. PTR Record (Pointer Record)
	- PTR records are used in reverse DNS lookups. 
	- They map an IP address to a domain name, providing the reverse mapping of an IP address to a hostname.

8. SRV Record (Service Record)
	- SRV records define the location of specific services within a domain.
	- They are used to locate services such as SIP (Session Initiation Protocol), LDAP (Lightweight Directory Access Protocol), and others.

9. SOA Record (Start of Authority Record)
	- It provides information about the authoritative DNS server for the domain, including contact information, refresh interval, retry interval, and other parameters.

10. CAA Record (Certification Authority Authorization Record)
	- CAA records specify which certificate authorities (CAs) are allowed to issue SSL/TLS certificates for a domain.
	- They help to enforce certificate security policies.