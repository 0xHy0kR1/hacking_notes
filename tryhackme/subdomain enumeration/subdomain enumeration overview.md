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