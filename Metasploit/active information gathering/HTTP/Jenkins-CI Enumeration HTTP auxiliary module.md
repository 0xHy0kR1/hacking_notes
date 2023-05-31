# Pre-requisite - [[Jankins]]
- It is a module is a scanner auxiliary module that allows you to enumerate information from a target Jenkins server.
- It can be used to gather information about jobs, nodes, users, and other details that could be useful for further penetration testing.
# Code - 
```python
msf6 auxiliary(scanner/http/http_put) > use auxiliary/scanner/http/jenkins_enum
msf6 auxiliary(scanner/http/jenkins_enum) > set RHOSTS 192.168.216.11
RHOSTS => 192.168.216.11
msf6 auxiliary(scanner/http/jenkins_enum) > set TARGETURI /
TARGETURI => /
msf6 auxiliary(scanner/http/jenkins_enum) > set RPORT 8484
RPORT => 8484
msf6 auxiliary(scanner/http/jenkins_enum) > run

[+] 192.168.216.11:8484   - Jenkins Version 1.637
[+] http://192.168.216.11:8484/ - /script does not require authentication (200)
[+] http://192.168.216.11:8484/ - /view/All/newJob does not require authentication (200)
[+] http://192.168.216.11:8484/ - /asynchPeople/ does not require authentication (200)
[+] http://192.168.216.11:8484/ - /systemInfo does not require authentication (200)
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed```