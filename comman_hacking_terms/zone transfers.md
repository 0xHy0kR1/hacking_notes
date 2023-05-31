
- Sometimes, one DNS server wants to get a copy of all the information from another DNS server, so it can have the same dictionary too. This is called a DNS zone transfer.
- In computer networking, a zone transfer query is a type of request made by a DNS (Domain Name System) server to transfer a copy of the DNS database from one[[ DNS server]] to another.
- When a DNS server receives a zone transfer request, it will send a copy of its zone file to the requesting DNS server.
- zone transfer queries can also pose a security risk if they are not properly secured. Attackers may use zone transfer queries to obtain sensitive information about a target domain, such as a list of all its subdomains and their IP addresses.
- As a result, many DNS servers are configured to restrict zone transfers to authorized servers only.
Related --> [[DNS Zone Transfer Misconfiguration]] --> [[Passive information gathering]] technique
