## Telnet introduction
- Telnet is an application protocol.
- It allows you, with the use of a telnet client, to connect to and execute commands on a remote machine that's hosting a telnet server. The client will then become a virtual terminal- allowing you to interact with the remote host.

## Replacement
Telnet sends all messages in clear text and has no specific security mechanisms, that's why it has been replaced by **SSH**.

## How does Telnet work?
The user connects to the server by using the Telnet protocol(entering **telnet** in terminal). The user then interacts with server using specific telnet commands.

## Syntax
```python
telnet [ip] [port]
```

