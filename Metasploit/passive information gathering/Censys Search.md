- Gather/censys_search is a Metasploit module that allows users to use the Censys Search Language to perform queries against the Hosts dataset using the Censys REST API.
- It help users find the specific information they are looking for. For example, users can search for hosts with specific open ports or operating systems, or for hosts that have recently.
- The module requires a Censys API ID and secret key to be configured in order to access the Censys API, and users must also agree to the Censys terms of service before using the module. With the appropriate permissions, the gather/censys_search module can be a powerful tool for performing reconnaissance and identifying potential vulnerabilities on target systems.
# code - 
```python
msf6 auxiliary(gather/censys_search) > use auxiliary/gather/censys_search 
msf6 auxiliary(gather/censys_search) > set CENSYS_UID f28c288b-2da2-4d3b-8961-59e25feb4a2f
CENSYS_UID => f28c288b-2da2-4d3b-8961-59e25feb4a2f
msf6 auxiliary(gather/censys_search) > set CENSYS_SECRET oKC4CVhyG4D0QlDOf9JsXvPzTSCQzxaF
CENSYS_SECRET => oKC4CVhyG4D0QlDOf9JsXvPzTSCQzxaF
msf6 auxiliary(gather/censys_search) > set QUERY codewithharry.com
QUERY => codewithharry.com
msf6 auxiliary(gather/censys_search) > run

[+] 139.59.75.126 - 22/SSH,80/HTTP,443/HTTP
[*] Auxiliary module execution completed
```