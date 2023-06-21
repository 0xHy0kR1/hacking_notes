## NFS introduction:
- NFS stands for "Network File System" and allows a system to share directories and files with others over a network.
- By using NFS, users and programs can access files on remote systems almost as if they were local files.
- It does this by mounting all, or a portion of a file system on a server. The portion of the file system that is mounted can be accessed by clients with whatever privileges are assigned to each file.

## How does NFS work?
1.  **Client and server:** NFS involves two main components: the client and the server. The client is the system that requests access to files, while the server is the system that stores the files and responds to client requests.
    
2. **Mounting:** On the client system, a directory on the server is mounted, which means it is associated with a mount point on the client's file system. The mount point acts as a gateway through which the client can access the files on the server.
    
3.  **NFS protocol:** The NFS protocol operates on top of the Remote Procedure Call (RPC) mechanism, allowing the client and server to communicate with each other. The NFS protocol defines a set of operations for file access, such as read, write, and directory operations.
    
4.  **File access:** When a client wants to access a file, it sends an NFS request to the server, specifying the file and the desired operation. The server processes the request and responds accordingly, either returning the requested data or performing the requested operation on the file.

If someone wants to access a file using NFS, an RPC call is placed to NFSD (the NFS daemon) on the server. This call takes parameters such as:
-  The file handle
-  The name of the file to be accessed
-  The user's, user ID
-  The user's group ID

## What runs NFS?
- Using the NFS protocol, you can transfer files between computers running Windows and other non-Windows operating systems, such as Linux, MacOS or UNIX.
- 