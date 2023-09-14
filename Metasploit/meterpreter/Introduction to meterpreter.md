- what we can do after we have exploited the target machine. Meterpreter provides us with many features that can ease our task of exploring the target machine.
- Meterpreter is a post-exploitation tool that is commonly used in penetration testing and ethical hacking to gain remote access to a compromised system.
## Why we can't use payload instead of meterpreter
- We have been using payloads in order to achieve specific results, but they have a major disadvantage.
- Payloads work by creating new processes in the compromised system. This can trigger alarms in antivirus programs and can be caught easily. Also, a payload is limited to perform only some specific tasks or execute specific commands that the shell can run. To overcome these difficulties, Meterpreter was created.
- When Meterpreter is used, it injects itself into a running process on the compromised system, typically a legitimate process such as explorer.exe or svchost.exe. This allows Meterpreter to run in memory without creating a new process that could be detected by antivirus software or other security measures.
- In contrast, when a payload is used to exploit a vulnerability, it typically creates a new process on the compromised system. This can be detected by security software and is generally less stealthy than using Meterpreter.
- Meterpreter uses encrypted communication with the target, which is another major advantage of using it.

## Stepwise representation of loading meterpreter:
							![[Stepwise_img_of_loading_meterpreter.jpeg]]
- In the first step, the exploit and first stage payload are sent to the target machine.
- After the exploitation, the stage establishes a TCP connection back to `msfconsole` on a given address and port.
- Next, `msfconsole` sends the second stage DLL injection payload.
- After successful injection, it sends the meterpreter DLL to establish a proper commucation channel.
- Lastly, Meterpreter loads extensions such as stdapi and priv. All these extensions are loaded over [[TLS]] using a [[TLV]] protocol.

## Advantages of Meterpreter
- It can migrate easily among process.
- It resides completely in memory, so it writes nothing to disk.
- It uses encrypted communications.
- It uses a channelized communication system so that we can work with several channels at a time.
- It provides a platform to write extensions quickly and easily.

## Meterpreter commands

**Typing `help` on any Meterpreter session will list all available commands.**
![[ms18.png]]
- Every version of Meterpreter will have different command options, so running the `help` command is always a good idea.
- meterpreter will run on the target system without loading any additional script or executable files.

**Meterpreter will provide you with three primary categories of tools;**
- Built-in commands
- Meterpreter tools
- Meterpreter scripting

**If you run the `help` command, you will see Meterpreter commands are listed under different categories.**
- Core commands
- File system commands
- Networking commands
- System commands
- User interface commands
- Webcam commands
- Audio output commands
- Elevate commands
- Password database commands
- Timestomp commands

**Note** - the list above was taken from the output of the `help` command on the Windows version of Meterpreter (windows/x64/meterpreter/reverse_tcp). These will be different for other Meterpreter versions.

**Below are some of the most commonly used Meterpreter commands** - 

**Core commands**
- `background`: Backgrounds the current session
- `exit`: Terminate the Meterpreter session
- `guid`: Get the session GUID (Globally Unique Identifier)  
- `help`: Displays the help menu
- `info`: Displays information about a Post module
- `irb`: Opens an interactive Ruby shell on the current session
- `load`: Loads one or more Meterpreter extensions
- `migrate`: Allows you to migrate Meterpreter to another process
- `run`: Executes a Meterpreter script or Post module
- `sessions`: Quickly switch to another session

**File system commands**
- `cd`: Will change directory
- `ls`: Will list files in the current directory (dir will also work)
- `pwd`: Prints the current working directory
- `edit`: will allow you to edit a file
- `cat`: Will show the contents of a file to the screen
- `rm`: Will delete the specified file
- `search`: Will search for files
- `upload`: Will upload a file or directory
- `download`: Will download a file or directory

**Networking commands**
- `arp`: Displays the host ARP (Address Resolution Protocol) cache
- `ifconfig`: Displays network interfaces available on the target system  
- `netstat`: Displays the network connections
- `portfwd`: Forwards a local port to a remote service
- `route`: Allows you to view and modify the routing table

**System commands**
- `clearev`: Clears the event logs
- `execute`: Executes a command
- `getpid`: Shows the current process identifier
- `getuid`: Shows the user that Meterpreter is running as
- `kill`: Terminates a process
- `pkill`: Terminates processes by name
- `ps`: Lists running processes
- `reboot`: Reboots the remote computer
- `shell`: Drops into a system command shell
- `shutdown`: Shuts down the remote computer
- `sysinfo`: Gets information about the remote system, such as OS

**Others Commands (these will be listed under different menu categories in the help menu)**
- `idletime`: Returns the number of seconds the remote user has been idle
- `keyscan_dump`: Dumps the keystroke buffer
- `keyscan_start`: Starts capturing keystrokes
- `keyscan_stop`: Stops capturing keystrokes
- `screenshare`: Allows you to watch the remote user's desktop in real time
- `screenshot`: Grabs a screenshot of the interactive desktop
- `record_mic`: Records audio from the default microphone for X seconds
- `webcam_chat`: Starts a video chat
- `webcam_list`: Lists webcams
- `webcam_snap`: Takes a snapshot from the specified webcam
- `webcam_stream`: Plays a video stream from the specified webcam
- `getsystem`: Attempts to elevate your privilege to that of local system
- `hashdump`: Dumps the contents of the SAM database

## Modules
**Once any additional tool is loaded using the `load` command, you will see new options on the `help` menu**
**Example** - 
![[ms19.png]]

![[ms20.png]]

**Note** - These will change according to the loaded menu, so running the `help` command after loading a module is always a good idea.