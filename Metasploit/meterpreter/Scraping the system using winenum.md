- Windows Local Enumeration(WinEnum)  script retrieves all kinds of information about the system including environment variables, network interfaces, routing, user accounts, and much more.
- The `winenum` script will run several commands such as `arp`, `net`, `netstat`, `netsh`, and `wmic` among other commands on the target machine and store result on `/root/.msf4/logs/scripts/winenum/` folder:
```python
meterpreter > run winenum
[*] Running Windows Local Enumeration Meterpreter Script
[*] New session on 192.168.216.11:445...
[*] Saving general report to /root/.msf4/logs/scripts/winenum/VAGRANT-2008R2_20230316.5343/VAGRANT-2008R2_20230316.5343.txt
[*] Output of each individual command is saved to /root/.msf4/logs/scripts/winenum/VAGRANT-2008R2_20230316.5343
[*] Checking if VAGRANT-2008R2 is a Virtual Machine ........
[*] 	UAC is Disabled
[*] Running Command List ...
[*] 	running command cmd.exe /c set
[*] 	running command netstat -ns
[*] 	running command arp -a
[*] 	running command ipconfig /all
[*] 	running command route print
[*] 	running command net view
[*] 	running command netstat -nao
[*] 	running command netstat -vb
[*] 	running command net accounts
[*] 	running command ipconfig /displaydns
[*] 	running command net session
[*] 	running command net group
[*] 	running command net share
[*] 	running command net localgroup administrators
[*] 	running command net group administrators
[*] 	running command net user
[*] 	running command net localgroup
[*] 	running command net view /domain
[*] 	running command netsh firewall show config
[*] 	running command tasklist /svc
[*] 	running command servermanagercmd.exe -q
[*] 	running command gpresult /SCOPE COMPUTER /Z
[*] 	running command gpresult /SCOPE USER /Z
[*] 	running command cscript /nologo winrm get winrm/config
[*] Running WMIC Commands ....
[*] 	running command wmic group list
[*] 	running command wmic logicaldisk get description,filesystem,name,size
[*] 	running command wmic volume list brief
[*] 	running command wmic netuse get name,username,connectiontype,localname
[*] 	running command wmic netlogin get name,lastlogon,badpasswordcount
[*] 	running command wmic share get name,path
[*] 	running command wmic netclient list brief
[*] 	running command wmic service list brief
[*] 	running command wmic nteventlog get path,filename,writeable
[*] 	running command wmic useraccount list
[*] 	running command wmic rdtoggle list
[*] 	running command wmic qfe
[*] 	running command wmic startup list full
[*] 	running command wmic product get name,version
[*] Extracting software list from registry
```
