## Telnet introduction
- Telnet is an application layer protocol.
- It allows you, with the use of a telnet client, to connect to and execute commands on a remote machine that's hosting a telnet server. The client will then become a virtual terminal- allowing you to interact with the remote host.
- Using Telnet, a user can log into another computer and access its terminal (console) to run programs, start batch processes, and perform system administration tasks remotely.

## Replacement
Telnet sends all messages in clear text and has no specific security mechanisms, that's why it has been replaced by **SSH**.

## How does Telnet work?
The user connects to the server by using the Telnet protocol(entering **telnet** in terminal). The user then interacts with server using specific telnet commands.

## Syntax
```python
telnet [ip] [port]
```

###### A user is connecting to the `telnetd`, a Telnet server. The steps are as follows:
 1. First, he is asked to provide his login name (username). We can see the user entering `frank`.
 2. Then, he is asked for the password, `D2xc9CgD`. The password is not shown on the screen; however, we display it below for demonstration purposes.
 3. Once the system checks his login credentials, he is greeted with a welcome message.
 4. And the remote server grants him a command prompt, `frank@bento:~$`. The `$` indicates that this is not a root terminal.
![[telnet7.png]]

#### We will use `telnet` instead of a web browser to request a file from the webserver.
   1. First, we connect to port 80 using `telnet MACHINE_IP 80`.
   2. Next, we need to type `GET /index.html HTTP/1.1` to retrieve the page `index.html` or `GET / HTTP/1.1` to retrieve the default page.
   3. Finally, you need to provide some value for the host like `host: telnet` and hit the Enter/Return key twice.

![[telnet8.png]]
   - In the console output below, we could recover the requested page along with a trove of information not usually displayed by the web browser.
   - If the page we requested is not found, we get error 404.
   - We need an HTTP server (webserver) and an HTTP client (web browser) to use the HTTP protocol.

Three popular choices for HTTP servers are:

- [Apache](https://www.apache.org/)
- [Internet Information Services (IIS)](https://www.iis.net/)
- [nginx](https://nginx.org/)

