- Whois essentially allows you to query who a domain name is registered to.
- A WHOIS server listens on TCP port 43 for incoming requests.
- The domain registrar is responsible for maintaining the WHOIS records for the domain names it is leasing

**The WHOIS server replies with various information related to the domain requested.**
- Registrar: Via which registrar was the domain name registered?
- Contact info of registrant: Name, organization, address, phone, among other things. (unless made hidden via a privacy service)
- Creation, update, and expiration dates: When was the domain name first registered? When was it last updated? And when does it need to be renewed?
- Name Server: Which server to ask to resolve the domain name?


## Syntax
```bash
whois <domain>
```

## Example
```bash
┌──(hyok㉿kali)-[~/Downloads]
└─$ whois facebook.com    
```
