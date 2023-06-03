- each process will have an ID associated with it, also known as its PID. The PID increments for the order In which the process starts. I.e. the 60th process will have a PID of 60.

## Viewing Processes
- We can use the friendly `ps` command to provide a list of the running processes.
![[process(ps).png]]

### 1. Viewing processes run by others(ps aux)
- To see the processes run by other users and those that don't run from a session (i.e. system processes), we need to provide **aux** to the `ps` command like so: `ps aux`.
![[processes(ps aux).png]]

### 2. real-time statistics about the processes(top)
- top gives you real-time statistics about the processes running on your system instead of a one-time view.
- These statistics will refresh every 10 seconds, but will also refresh when you use the arrow keys to browse the various rows.
![[processes(top).png]]

### Killing a process(kill PID)
- To `kill` command or process and the associated PID that we wish to kill. i.e., to kill PID 1337.
![[killing_process_information.png]]

#### Below are some of the signals that we can send to a process when it is killed:
- **SIGTERM** - Kill the process, but allow it to do some cleanup tasks beforehand
- **SIGKILL** - Kill the process - doesn't do any cleanup after the fact
- **SIGSTOP** - Stop/suspend a process

## How do Processes Start?
- The Operating System (OS) uses namespaces to ultimately split up the resources available on the computer to (such as CPU, RAM and priority) processes.
- Processes within that slice will have access to a certain amount of computing power.
- Namespaces are great for security as it is a way of isolating processes from another -- only those that are in the same namespace will be able to see each other.
- The process with an ID of 0 is a process that is started when the system boots.
- This process is the system's init on Ubuntu, such as **systemd**, which is used to provide a way of managing a user's processes and sits in between the operating system and the user. Any program or piece of software that we want to start will start as what's known as a child process of **systemd**. This means that it is controlled by **systemd**, but will run as its own process

## Starting processes on boot
#### systemctl
- this command allows us to interact with the **systemd** process/daemon.

#### Syntax 
```bash
systemctl [option] [service]
```

#### Example
```bash
┌──(hyok㉿kali)-[~]
└─$ systemctl start apache2         
```

**We can four options with `systemctl`:**
- Start
- Stop
- Enable
- Disable

## Executing processes on background 
### & operator
![[processes_background.png]]

### `Ctrl + Z`
![[process_background_ctrlz.png]]
## Executing processes on foreground(fg)
![[processes_foreground.png]]
