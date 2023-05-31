- The module can be used to gather information about the target device, such as its configuration settings, running services, and other system information.
- The SNMP_enum module is an auxiliary module, which means that it does not require any authentication to be performed on the target device.
- We can also gather loads of information using SNMP scanning modules, such as open ports, services, hostnames, processes, and uptime.
# Code - 
```python
msf6 auxiliary(scanner/snmp/snmp_login) > use auxiliary/scanner/snmp/snmp_enum
msf6 auxiliary(scanner/snmp/snmp_enum) > set RHOSTS 192.168.216.11
RHOSTS => 192.168.216.11
msf6 auxiliary(scanner/snmp/snmp_enum) > run

[+] 192.168.216.11, Connected.

[*] System information:
--------------------------------------SNIP-----------------------------------
```
