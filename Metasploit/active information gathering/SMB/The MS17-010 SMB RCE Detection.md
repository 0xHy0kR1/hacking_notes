# Pre-requisite - [[MS17-010 vulnerability]]
# Pre-requisite - [[IPC$ tree]]
- It is used to identify Windows computers that are vulnerable to the MS17-010 exploit.
- MS17-010 is a critical vulnerability in the SMBv1 protocol that allows remote attackers to execute arbitrary code on a target computer without authentication.
- The scanner/smb/smb_ms17_010 module uses several techniques to identify vulnerable Windows computers on a network, including sending specially crafted SMB packets to a target computer and analyzing the response to determine whether the computer is vulnerable to the MS17-010 exploit.
# Code - 
```python
msf6 > use auxiliary/scanner/smb/smb_ms17_010
msf6 auxiliary(scanner/smb/smb_ms17_010) > set RHOSTS 192.168.216.11
RHOSTS => 192.168.216.11
msf6 auxiliary(scanner/smb/smb_ms17_010) > set SMBPass vagrant
SMBPass => vagrant
msf6 auxiliary(scanner/smb/smb_ms17_010) > set SMBUser vagrant
SMBUser => vagrant
msf6 auxiliary(scanner/smb/smb_ms17_010) > run

[+] 192.168.216.11:445    - Host is likely VULNERABLE to MS17-010! - Windows Server 2008 R2 Standard 7601 Service Pack 1 x64 (64-bit)
[*] 192.168.216.11:445    - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed

```