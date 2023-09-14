- The TELNET (Teletype Network) protocol was developed in 1969 to communicate with a remote system via a command-line interface (CLI).
- the command `telnet` uses the TELNET protocol for remote administration.
- The default port used by telnet is 23.
- From a security perspective, `telnet` sends all the data, including usernames and passwords, in cleartext. The secure alternative is SSH (Secure SHell) protocol.
- Knowing that telnet client relies on the TCP protocol, you can use Telnet to connect to any service and grab its banner.
- Using `telnet MACHINE_IP PORT`, you can connect to any service running on TCP

## Connecting a web server using Telnet - 
   - Let’s say we want to discover more information about a web server, listening on port 80. We connect to the server at port 80, and then we communicate using the HTTP protocol.
   - You don’t need to dive into the HTTP protocol; you just need to issue `GET / HTTP/1.1`. To specify something other than the default index page, you can issue `GET /page.html HTTP/1.1`, which will request `page.html`.
   - We also specified to the remote web server that we want to use HTTP version 1.1 for communication.
   - To get a valid response, instead of an error, you need to input some value for the host `host: example` and hit enter twice.

**Executing these steps will provide the requested index page.**
![[active_recon5.png]]

Of particular interest for us is discovering the type and version of the installed web server, `Server: nginx/1.6.2`