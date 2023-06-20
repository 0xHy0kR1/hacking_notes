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