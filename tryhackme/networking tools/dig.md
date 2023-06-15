- When you visit a website in your web browser this all happens automatically, but we can also do it manually with a tool called `dig`
- Dig allows us to manually query recursive DNS servers of our choice for information about domains:

## Syntax
```bash 
dig <domain> @<dns-server-ip>
```

## Example
```bash
┌──(hyok㉿kali)-[~/Downloads]
└─$ dig google@8.8.8.8
```
