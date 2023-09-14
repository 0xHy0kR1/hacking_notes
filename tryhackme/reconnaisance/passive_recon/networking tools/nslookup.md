Find the IP address of a domain name using `nslookup`, which stands for Name Server Look Up.

## Syntax
```shell
nslookup DOMAIN_NAME
```
Or
```shell
nslookup OPTIONS DOMAIN_NAME SERVER
```
- OPTIONS contains the query type as shown in the table below. For instance, you can use `A` for IPv4 addresses and `AAAA` for IPv6 addresses.
- DOMAIN_NAME is the domain name you are looking up.
- - SERVER is the DNS server that you want to query. You can choose any local or public DNS server to query. Cloudflare offers `1.1.1.1` and `1.0.0.1`, Google offers `8.8.8.8` and `8.8.4.4`, and Quad9 offers `9.9.9.9` and `149.112.112.112`. There are many [more public DNS servers](https://duckduckgo.com/?q=public+dns) that you can choose from if you want alternatives to your ISP’s DNS servers.

![[nettools2.png]]


## Example
```shell
┌──(hoax㉿kali)-[~/thm]
└─$ nslookup tryhackme.com
```
Or
**Including options** - 
```shell
nslookup -type=A tryhackme.com 1.1.1.1
```

and

```shell
nslookup -type=a tryhackme.com 1.1.1.1
```
as it is case-insensitive

**For email servers** - 
```shell
nslookup -type=MX tryhackme.com
```

![[nettools3.png]]
We can see that tryhackme.com’s current email configuration uses Google. Since MX is looking up the Mail Exchange servers, we notice that when a mail server tries to deliver email `@tryhackme.com`, it will try to connect to the `aspmx.l.google.com`, which has order 1. If it is busy or unavailable, the mail server will attempt to connect to the next in order mail exchange servers, `alt1.aspmx.l.google.com` or `alt2.aspmx.l.google.com`.


![[nettools1.png]]
