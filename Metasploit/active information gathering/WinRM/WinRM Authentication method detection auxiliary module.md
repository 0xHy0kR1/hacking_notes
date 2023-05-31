# Pre-requisite - [[WinRm]] and [[WinRM configuration on windows 2008]]
- The scanner/winrm/winrm_auth_methods module is a Metasploit module that can be used to scan a network for Windows Remote Management (WinRM) services and identify the authentication methods that are enabled.

# Code - 
```python
msf6 > use auxiliary/scanner/winrm/winrm_auth_methods 
msf6 auxiliary(scanner/winrm/winrm_auth_methods) > set RHOSTS 192.168.216.11
RHOSTS => 192.168.216.11
msf6 auxiliary(scanner/winrm/winrm_auth_methods) > run

[+] 192.168.216.11:5985: Negotiate protocol supported
[+] 192.168.216.11:5985: Basic protocol supported
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed```