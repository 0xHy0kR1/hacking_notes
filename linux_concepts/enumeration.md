>The "hostname" command will return the hostname of the target machine.
```sh
hostname
```


>The "uname -a" Will print system information giving us additional detail about the kernel used by the system.
```sh
uname -a
```


>The proc filesystem (procfs) provides information about the target system processes.
```sh
/proc/version
```
Looking at `/proc/version` may give you information on the kernel version and additional data such as whether a compiler (e.g. GCC) is installed.


>Systems can also be identified by looking at the `/etc/issue` file.
```sh
/etc/issue
```
This file usually contains some information about the operating system but can easily be customized or changed.


>The `ps` command is an effective way to see the running processes on a Linux system.
```sh
ps
```

**The output of the `ps` (Process Status) will show the following;**
- PID: The process ID (unique to the process)
- TTY: Terminal type used by the user
- Time: Amount of CPU time used by the process (this is NOT the time this process has been running for)
- CMD: The command or executable running (will NOT display any command line parameter)

**The “ps” command provides a few useful options.**

>View all running processes
```sh
ps -A
```

>View process tree (see the tree formation until `ps axjf` is run below)
```sh
ps axjf
```

![[privesc1.png]]

>The `aux` option will show processes for all users (a), display the user that launched the process (u), and show processes that are not attached to a terminal (x).
```sh
ps aux
```


>The `env` command will show environmental variables.
```sh
env
```
![[privesc2.png]]
  

The PATH variable may have a compiler or a scripting language (e.g. Python) that could be used to run code on the target system or leveraged for privilege escalation.


>The `sudo -l` command can be used to list all commands your user can run using `sudo`.
```sh
sudo -l
```


>The `id` command will provide a general overview of the user’s privilege level and group memberships.
```sh
id your_user_name
```


>Reading the `/etc/passwd` file can be an easy way to discover users on the system.
```sh
/etc/passwd
```
![[privesc3.png]]

>While the output can be long and a bit intimidating, it can easily be cut and converted to a useful list for brute-force attacks.
```sh
cat /etc/passwd | cut -d ":" -f 1
```
![[privesc4.png]]
Remember that this will return all users, some of which are system or service users that would not be very useful.

>Grep for “home” as real users will most likely have their folders under the “home” directory.
```sh
cat /etc/passwd | grep home
```
![[privesc5.png]]


>Looking at earlier commands with the `history` command can give us some idea about the target system such as passwords or usernames.
```sh
history
```


>The `ifconfig` command will give us information about the network interfaces of the system.
```sh
ifconfig
```
The target system may be a pivoting point to another network. The example below shows the target system has three interfaces (eth0, tun0, and tun1). Our attacking machine can reach the eth0 interface but can not directly access the two other networks.
![[privesc6.png]]

>This can be confirmed using the `ip route` command to see which network routes exist.
```sh
ip route
```
![[privesc7.png]]


#### netstat
  The `netstat` command can be used with several different options to gather information on existing connections.
  
>shows all listening ports and established connections.
```sh
netstat -a 
```

>The below can also be used to list TCP or UDP protocols respectively.
```sh
netstat -at
```

```sh
netstat -au
```

>list ports in “listening” mode.
```sh
netstat -l
```
These ports are open and ready to accept incoming connections. 

>The below can be used with the “t” option to list only ports that are listening using the TCP protocol
```sh
netstat -lt
```

>List network usage statistics by protocol.
```sh
netstat -s
```
This can also be used with the `-t` or `-u` options to limit the output to a specific protocol.
![[privesc8.png]]

>List connections with the service name and PID information.
```sh
netstat -tp
```
![[privesc9.png]]

>This can also be used with the `-l` option to list listening ports
```sh
netstat -ltp
```
![[privesc10.png]]

>Shows interface statistics. We see below that “eth0” and “tun0” are more active than “tun1”.
```sh
netstat -i 
```
![[privesc11.png]]

>The `netstat` usage you will probably see most often in blog posts, write-ups, and courses is as follows:
```sh
netstat -ano
```
- `-a`: Display all sockets
- `-n`: Do not resolve names
- `-o`: Display timers
![[privesc12.png]]

### find Command

**Below are some useful examples for the “find” command.**
  - `find . -name flag1.txt`: find the file named “flag1.txt” in the current directory
  - `find /home -name flag1.txt`: find the file names “flag1.txt” in the /home directory
  - `find / -type d -name config`: find the directory named config under “/”
  - `find / -type f -perm 0777`: find files with the 777 permissions (files readable, writable, and executable by all users)
  - `find / -perm a=x`: find executable files
  - `find / -user frank`: find all files for user “frank” under “/home”
  - `find / -mtime 10`: find files that were modified in the last 10 days
  - `find / -atime 10`: find files that were accessed in the last 10 day
  - `find / -cmin -60`: find files changed within the last hour (60 minutes)
  - `find / -amin -60`: find files accesses within the last hour (60 minutes)
  - `find / -size 50M`: find files with a 50 MB size

**This command can also be used with (+) and (-) signs to specify a file that is larger or smaller than the given size.**
![[privesc13.png]]

**Note** - It is important to note that the “find” command tends to generate errors which sometimes makes the output hard to read. This is why it would be wise to use the “find” command with “-type f 2>/dev/null” to redirect errors to “/dev/null” and have a cleaner output (below).
![[privesc14.png]]

**Folders and files that can be written to or executed from:**
   - `find / -writable -type d 2>/dev/null` : Find world-writeable folders
   - `find / -perm -222 -type d 2>/dev/null`: Find world-writeable folders
   - `find / -perm -o w -type d 2>/dev/null`: Find world-writeable folders
   - `find / -perm -o x -type d 2>/dev/null` : Find world-executable folders

**Find development tools and supported languages:**
   - `find / -name perl*`
   - `find / -name python*`
   - `find / -name gcc*`

>**Find files that have the SUID bit set**
```sh
find / -perm -u=s -type f 2>/dev/null
```

>**Find files that have the SUID and SGID bit set**
```sh
find / -type f -perm -04000 -ls 2>/dev/null
```

#### Automated Enumeration Tools
- **LinPeas**: [https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS)
- **LinEnum:** [https://github.com/rebootuser/LinEnum](https://github.com/rebootuser/LinEnum)[](https://github.com/rebootuser/LinEnum)
- **LES (Linux Exploit Suggester):** [https://github.com/mzet-/linux-exploit-suggester](https://github.com/mzet-/linux-exploit-suggester)
- **Linux Smart Enumeration:** [https://github.com/diego-treitos/linux-smart-enumeration](https://github.com/diego-treitos/linux-smart-enumeration)
- **Linux Priv Checker:** [https://github.com/linted/linuxprivchecker](https://github.com/linted/linuxprivchecker)

**The Kernel exploit methodology is simple;**
  1. Identify the kernel version
  2. Search and find an exploit code for the kernel version of the target system
  3. Run the exploit

Sources such as [https://www.linuxkernelcves.com/cves](https://www.linuxkernelcves.com/cves) can also be useful.
