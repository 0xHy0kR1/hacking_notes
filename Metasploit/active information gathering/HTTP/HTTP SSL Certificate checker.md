- This module allows you to scan a target web server to obtain information about its SSL/TLS certificate, such as the certificate's issuer, subject, and expiration date.
- By using this module, you can quickly determine whether the target web server is using HTTPS and obtain additional details about its SSL/TLS configuration.
# Code -
```python
msf6 auxiliary(scanner/snmp/snmp_enum) > use auxiliary/scanner/http/cert
msf6 auxiliary(scanner/http/cert) > set RHOSTS 188.184.21.108
RHOSTS => 188.184.21.108
msf6 auxiliary(scanner/http/cert) > run

[*] 188.184.21.108:443    - 188.184.21.108 - 'www.cern.ch' : '2023-01-16 00:00:00 UTC' - '2024-01-16 23:59:59 UTC'
[*] 188.184.21.108:443    - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```