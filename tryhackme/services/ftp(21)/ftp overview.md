File Transfer Protocol (FTP) is, as the name suggests , a protocol used to allow remote transfer of files over a network. It uses a client-server model.

## How does FTP work?
**A typical FTP session operates using two channels:**
- a command (sometimes called the control) channel
- a data channel.

1. command channel
	- the command channel is used for transmitting commands as well as replies to those commands. While the session is open, the client may execute FTP commands on the server.

2. Data channel
	- the data channel is used for transferring data.

## Active vs Passive
**The FTP server may support either Active or Passive connections, or both.**

- In an Active FTP connection, the client opens a port and listens. The server is required to actively connect to it.
- In a Passive FTP connection, the server opens a port and listens (passively) and the client connects to it.

### Connecting to FTP using Telnet

   1. We connected to an FTP server using a Telnet client. Since FTP servers listen on port 21 by default, we had to specify to our Telnet client to attempt connection to port 21 instead of the default Telnet port.
   2. We needed to provide the username with the command `USER frank`.
   3. Then, we provided the password with the command `PASS D2xc9CgD`.
   4. Because we supplied the correct username and password, we got logged in.

#### Commands after connection
   1. **STAT**
	- A command like `STAT` can provide some added information.

   2. **SYST**
	- The `SYST` command shows the System Type of the target (UNIX in this case).

   3. **PASV**
	- `PASV` switches the mode to passive. 
	- `PASV` switches the mode to passive. It is worth noting that there are two modes for FTP:
		- Active: In the active mode, the data is sent over a separate channel originating from the FTP server’s port 20.
		- Passive: In the passive mode, the data is sent over a separate channel originating from an FTP client’s port above port number 1023.
	
   4. **TYPE A** 
       - The command `TYPE A` switches the file transfer mode to ASCII
	
   
   5. **TYPE I**
      - `TYPE I` switches the file transfer mode to binary.

**Note** - we cannot transfer a file using a simple client such as Telnet because FTP creates a separate connection for file transfer.

![[ftp5.png]]

Examples of FTP server software include:

- [vsftpd](https://security.appspot.com/vsftpd.html)
- [ProFTPD](http://www.proftpd.org/)
- [uFTP](https://www.uftpserver.com/)

**Note** - 
You can use an FTP client with GUI such as [FileZilla](https://filezilla-project.org/). Some web browsers also support FTP protocol.

