- Before we can use resource scripts in our Meterpreter session.
-  We first need to create the directory where we will be placing the scripts, for which we will use the `mkdir` command with the `-p` option so that it will create all the parent directories:

## For the first script, we will start with some basic commands to get system information:
```python
┌──(root㉿kali)-[/home/hyok]
└─# cat > ~/.msf4/scripts/resource/meterpreter/systeminfo.rc

sysinfo
getuid
getpid
getwd
^C
```

## Let's try the resource script in a Meterpreter session and see how it works:
```python
meterpreter > resource systeminfo.rc
[*] Processing /root/.msf4/scripts/resource/meterpreter/systeminfo.rc for ERB directives.
resource (/root/.msf4/scripts/resource/meterpreter/systeminfo.rc)> sysinfo
Computer        : VAGRANT-2008R2
OS              : Windows 2008 R2 (6.1 Build 7601, Service Pack 1).
Architecture    : x64
System Language : en_US
Domain          : WORKGROUP
Logged On Users : 2
Meterpreter     : x86/windows
resource (/root/.msf4/scripts/resource/meterpreter/systeminfo.rc)> getuid
Server username: NT AUTHORITY\SYSTEM
resource (/root/.msf4/scripts/resource/meterpreter/systeminfo.rc)> getpid
Current pid: 4444
resource (/root/.msf4/scripts/resource/meterpreter/systeminfo.rc)> getwd
C:\Windows\system32
```
