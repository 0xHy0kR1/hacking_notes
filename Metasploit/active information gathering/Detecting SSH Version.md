# Pre-requisite - [[SSH]]
- The scanner/ssh/ssh_version module is a scanner that is used to detect the version of the SSH protocol that is running on a remote system
- The module works by connecting to a remote SSH server and sending a series of probes to identify the version of the SSH protocol that is running.
# Code - 
```python
msf6 auxiliary(scanner/smb/smb_ms17_010) > use auxiliary/scanner/ssh/ssh_version
msf6 auxiliary(scanner/ssh/ssh_version) > set RHOSTS 192.168.216.11
RHOSTS => 192.168.216.11
msf6 auxiliary(scanner/ssh/ssh_version) > run

[+] 192.168.216.11:22     - SSH server version: SSH-2.0-OpenSSH_7.1 ( service.version=7.1 service.vendor=OpenBSD service.family=OpenSSH service.product=OpenSSH service.cpe23=cpe:/a:openbsd:openssh:7.1 service.protocol=ssh fingerprint_db=ssh.banner )
[*] 192.168.216.11:22     - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed```