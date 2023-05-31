# Description 
This module can be used to gather information about a domain from a given DNS server by performing various DNS queries such as [[zone transfers]],[[ reverse lookups]], [[SRV record brute forcing]], and other techniques.
## code - 
```python
msf > use auxiliary/gather/enum_dns 
msf auxiliary(enum_dns) > set DOMAIN packtpub.com 
DOMAIN => packtpub.com 
msf auxiliary(enum_dns) > set THREADS 10 
THREADS => 10 
msf auxiliary(enum_dns) > run
```

## Some extra information - 
1. We can use the info command to display information about the module.
2. To run the module, we need to set the domain name, and to make it run a bit faster, we will set the thread number to 10: