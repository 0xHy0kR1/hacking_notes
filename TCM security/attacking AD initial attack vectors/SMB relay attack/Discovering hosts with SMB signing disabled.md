1. With nmap nse script to discover it:
```python
┌──(hyok㉿kali)-[~]
└─$ sudo nmap --script=smb2-security-mode 192.168.1.0/24
```

1. Output for domain controller:
	![[SMB_relay_attack1.png]]
SMB relay attack is not possible

2. Output to fcastle:
	![[SMB_relay_attack2.png]]
smb relay attack is possible('Message signing enabled but not required' meaning we can perform a SMB relay attack as signing is not required.)

3. Output to pparker:
	![[SMB_relay_attack3.png]]
	SMB relay attack is possible
	('Message signing enabled but not required' meaning we can perform a SMB relay attack as signing is not required.)