# Pre-requisite - [[SMB]]
- The SMB Version Detection auxiliary module displays the SMB version for each target system:
# Code - 
```python
msf6 > use auxiliary/scanner/smb/smb_version
msf6 auxiliary(scanner/smb/smb_version) > set RHOSTS 192.168.216.11
RHOSTS => 192.168.216.11
msf6 auxiliary(scanner/smb/smb_version) > run

[*] 192.168.216.11:445    - SMB Detected (versions:1, 2) (preferred dialect:SMB 2.1) (signatures:optional) (uptime:39m 39s) (guid:{d82b1a6d-b657-4a62-b4b2-39511412b4da}) (authentication domain:VAGRANT-2008R2)Windows 2008 R2 Standard SP1 (build:7601) (name:VAGRANT-2008R2) (workgroup:WORKGROUP)
[+] 192.168.216.11:445    -   Host is running SMB Detected (versions:1, 2) (preferred dialect:SMB 2.1) (signatures:optional) (uptime:39m 39s) (guid:{d82b1a6d-b657-4a62-b4b2-39511412b4da}) (authentication domain:VAGRANT-2008R2)Windows 2008 R2 Standard SP1 (build:7601) (name:VAGRANT-2008R2) (workgroup:WORKGROUP)
[*] 192.168.216.11:       - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```
