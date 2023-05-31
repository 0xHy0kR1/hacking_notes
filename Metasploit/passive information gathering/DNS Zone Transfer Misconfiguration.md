A misconfigured DNS Zone Transfer will lead to leaks of user names and relevant IP addresses.
# The misconfigured DNS Zone Transfer can be defined in 2 types - 
## 1. [[AXFR - Full Duplex DNS Zone Transfer]]
## 2. [[IXFR - Partial Duplex DNS Zone Transfer]]
# To track a misconfigured DNS Zone Transfer, I'm going to use **nslookup** in Microsoft Windows:
[[misconfigured DNS Zone Transfer.jpg]]
1. Type below one and press Enter.
```python
nslookup -type=ns<URL>
Example - C:\WINDOWS\system32>nslookup -type=ns codewithharry.com
```
Explaination - The nslookup reveals the name servers of the respective URL, note down the nameservers.

1. Just type the "nslookup" to go into the command mode of nslookup
2. Then type `server <name server>` and press Enter
3. Then type `set type=any` to  send the queries regarding the complete DNS zone transfer information.
4. 1.  Then type "**ls -d <URL>", if the domain is having DNS Zone Transfer Misconfiguration, then it will show up.