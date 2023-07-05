## SMB Introduction
- SMB stands for **Server Message Block Protocol**. 
- It is a client-server communication protocol used for sharing access to files, printers, serial ports and other resources on a network.
- The SMB protocol is known as a response-request protocol, meaning that it transmits multiple messages between the client and server to establish a connection.
- Clients connect to servers using TCP/IP (actually NetBIOS over TCP/IP as specified in RFC1001 and RFC1002), NetBEUI or IPX/SPX.

## How does SMB work?
![[SMB1.png]]
Once they have established a connection, clients can then send commands (SMBs) to the server that allow them to access shares, open files, read and write files, and generally do all the sort of things that you want to do with a file system.

## What runs SMB?
- Microsoft Windows operating systems since Windows 95 have included client and server SMB protocol support.
- Samba, an open source server that supports the SMB protocol, was released for Unix systems.

## Regular SMB exchange between client and server:
1. _NetBIOS session established between the client and the server,_
2. _Server and client negotiation the SMB protocol dialect,_
3. _Client logs on to the server with the proper credentials,_
4. _Client will connect to a shared resource hosted on the server (i.e. wireless printer),_
5. _Client opens a file on the share, and,_
6. _Client reads or edits the requested resource. That would be a top-level overview of what happens during a regular SMB exchange_.