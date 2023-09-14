Subdomain enumeration is the process of finding valid subdomains for a domain.
We will explore three different subdomain enumeration methods: Brute Force, OSINT (Open-Source Intelligence) and Virtual Host.

## OSINT
### SSL/TLS certificates:
When an SSL/TLS (Secure Sockets Layer/Transport Layer Security) certificate is created for a domain by a CA (Certificate Authority), CA's take part in what's called "Certificate Transparency (CT) logs". These are publicly accessible logs of every SSL/TLS certificate created for a domain name. The purpose of Certificate Transparency logs is to stop malicious and accidentally made certificates from being used. 

We can use this service to our advantage to discover subdomains belonging to a domain.

sites like --> [https://crt.sh](http://crt.sh) and [https://ui.ctsearch.entrust.com/ui/ctsearchui](https://ui.ctsearch.entrust.com/ui/ctsearchui)

### Finding subdomain in google:
![[web_terms6.png]]

#### Virtual hosts:
- Some subdomains aren't always hosted in publically accessible DNS results, such as administration portals. 
- Instead, the DNS record could be kept on a private DNS server or recorded on the developer's machines in their /etc/hosts file (or c:\windows\system32\drivers\etc\hosts file for Windows users) which maps domain names to IP addresses.
Try the following command against the Acme IT Support machine to try and discover a new subdomain.
```python
user@machine$ ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://10.10.248.110
```
	- -w switch to specify the wordlist
	- -H switch adds/edits a header (in this instance, the Host header)
	- FUZZ - the FUZZ keyword in the space where a subdomain would normally go, and this is where we will try all the options from the wordlist.

printing subdomains based on page size:
```python
user@machine$ ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://10.10.248.110 -fs {size}
```
	- -fs --> It tells ffuf to ignore any results that are of the specified size.


## Subdomain enumeration using DNSDumpster
- It is an online service that offers detailed answers to DNS queries, such as [DNSDumpster](https://dnsdumpster.com/)
- If we search DNSDumpster for `tryhackme.com`, we will discover the subdomain `blog.tryhackme.com`, which a typical DNS query cannot provide.
- In addition, DNSDumpster will return the collected DNS information in easy-to-read tables and a graph.
- We can also see the MX records; DNSDumpster resolved all five mail exchange servers to their respective IP addresses and provided more information about the owner and location. Finally, we can see TXT records.
![[dnsdumpster1.png]]

**DNSDumpster will also represent the collected information graphically. DNSDumpster displayed the data from the table earlier as a graph. You can see the DNS and MX branching to their respective servers and also showing the IP addresses.**
![[dnsdumpster2.png]]

**There is currently a beta feature that allows you to export the graph as well. You can manipulate the graph and move blocks around if needed.**
![[dnsdumpster3.png]]