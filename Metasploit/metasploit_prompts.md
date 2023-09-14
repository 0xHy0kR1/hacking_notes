##### 1. **The regular command prompt:** 
You can not use Metasploit commands here.
```python
root@ip-10-10-XX-XX:~#
```

##### 2. The msfconsole prompt:
- As you can see, no context is set here, so context-specific commands to set parameters and run modules can not be used here.
```python
msf6 >
```

##### 3. A context prompt:
- Once you have decided to use a module and used the set command to chose it, the msfconsole will show the context.
- You can use context-specific commands (e.g. set RHOSTS 10.10.x.x) here.
```python
msf6 exploit(windows/smb/ms17_010_eternalblue) >
```

##### 4. Meterpreter prompt:
Meterpreter agent was loaded to the target system and connected back to you. You can use Meterpreter specific commands here.
```python
meterpreter >
```

##### 5. A shell on the target system:
- Once the exploit is completed, you may have access to a command shell on the target system.
- This is a regular command line, and all commands typed here run on the target system.
```python
C:\Windows\system32>
```

## Metasploit context prompt commands - 
- You can also clear any parameter value using the `unset` command or clear all set parameters with the `unset all` command.
```python
msf6 exploit(windows/smb/ms17_010_eternalblue) > unset all
```

- The `setg` command is used like the set command. The difference is that if you use the `set` command to set a value using a module and you switch to another module, you will need to set the value again. The `setg` command allows you to set the value so it can be used by default across different modules.
- The `setg` command sets a global value that will be used until you exit Metasploit or clear it using the `unsetg` command.
```python
msf6 exploit(windows/smb/ms17_010_eternalblue) > setg rhosts 10.10.165.39
rhosts => 10.10.165.39
```

- You can clear any value set with `setg` using `unsetg`.

- The `exploit -z` command will run the exploit and background the session as soon as it opens.
![[ms15.png]]

## Sessions
- Once a vulnerability has been successfully exploited, a session will be created. This is the communication channel established between the target system and Metasploit.
- You can use the `background` command to background the session prompt and go back to the msfconsole prompt.
```python
meterpreter > background
[*] Backgrounding session 2...
msf6 exploit(windows/smb/ms17_010_eternalblue) > 
```
Alternatively, `CTRL+Z` can be used to background sessions.

**The `sessions` command can be used from the msfconsole prompt or any context to see the existing sessions.**
![[ms16.png]]

**To interact with any session, you can use the `sessions -i` command followed by the desired session number.**
![[ms17.png]]
