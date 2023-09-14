- Netcat supports both TCP and UDP protocols.
- It can function as a client that connects to a listening port; alternatively, it can act as a server that listens on a port of your choice.
- First, you can connect to a server, as you did with Telnet, to collect its banner using `nc 10.10.89.171 PORT`.

![[active_recon6.png]]
**Note** - You might need to press SHIFT+ENTER after the GET line.

**Explaination to above** - 
  - In the terminal shown above, we used netcat to connect to 10.10.89.171 port 80 using `nc 10.10.89.171 80`.
  - Next, we issued a get for the default page using `GET / HTTP/1.1`.
  - Finally, we need to give a name to our host, so we added on a new line, `host: netcat`; you can name your host anything as this has no impact on this exercise.
  - Based on the output `Server: nginx/1.6.2` we received, we can tell that on port 80, we have Nginx version 1.6.2 listening for incoming connections.

#### Listening on port
```python
nc -lvnp 4444
```
It is equivalent to `nc -v -l -n -p 1234`.

- The exact order of the letters does not matter as long as the port number is preceded directly by `-p`.
![[active_recon7.png]]

**Notes:** - 
- the option `-p` should appear just before the port number you want to listen on.
- the option `-n` will avoid DNS lookups and warnings.
- port numbers less than 1024 require root privileges to listen on.

On the _client_-side, you would issue `nc 10.10.89.171 PORT_NUMBER`. Here is an example of using `nc` to echo. After you successfully establish a connection to the server, whatever you type on the client-side will be echoed on the server-side and vice versa.

 