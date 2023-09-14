- For more advanced DNS queries and additional functionality, you can use `dig`, the acronym for “Domain Information Groper.
- Dig allows us to manually query recursive DNS servers of our choice for information about domains:
- Let’s use `dig` to look up the MX records and compare them to `nslookup`.
- We can use `dig DOMAIN_NAME`, but to specify the record type, we would use `dig DOMAIN_NAME TYPE`.
- Optionally, we can select the server we want to query using `dig @SERVER DOMAIN_NAME TYPE`.
	- SERVER is the DNS server that you want to query.
	- DOMAIN_NAME is the domain name you are looking up.
	- TYPE contains the DNS record type, as shown in the table provided earlier.

## Syntax
```bash 
dig <domain> @<dns-server-ip>
```

## Example
```bash
┌──(hyok㉿kali)-[~/Downloads]
└─$ dig google@8.8.8.8
```

![[nettools4.png]]
A quick comparison between the output of `nslookup` and `dig` shows that `dig` returned more information, such as the TTL (Time To Live) by default. If you want to query a `1.1.1.1` DNS server, you can execute `dig @1.1.1.1 tryhackme.com MX`.

