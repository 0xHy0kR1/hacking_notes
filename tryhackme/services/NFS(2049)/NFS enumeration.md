## Pre-requisite --> [[tryhackme/services/enumeration]]

## NFS-Common
- It is important to have this package installed on any machine that uses NFS, either as client or server.
- It includes programs such as: **lockd, statd**, **showmount**, **nfsstat,** **gssd**, **idmapd** and **mount.nfs**.
- Primarily, we are concerned with "showmount" and "mount.nfs" as these are going to be most useful to us when it comes to extracting information from the NFS share.
- You can install **nfs-common** using sudo apt install nfs-common

## Mounting NFS shares
**Here's a step-by-step explanation of the process:
1. **Install NFS client software**:
	- Ensure that the client system has the necessary NFS client software installed.
	- This software allows the client to communicate with NFS servers and handle the NFS protocol.

2. **Create a mount point:**
	- On the client system, choose a directory where you want to access the shared files. This directory will act as a mount point.
	- You can create a new directory specifically for this purpose or use an existing one.
**Example** - 
```python
root@ip-10-10-0-197:~# mkdir /tmp/mount
```

3. **Identify the NFS server:**
	- Obtain the hostname or IP address of the NFS server that contains the shared files you want to access.

4. **Mount the NFS share:**
	- Use the `mount` command on the client system to mount the NFS share.
```python
mount -t nfs 10.10.0.197:/home /tmp/mount -nolock
```

**Syntax** - 
```python
mount -t nfs <NFS server>:<remote directory> <local directory> -nolock
```

	 -t nfs --> Type of device to mount, then specifying that it's NFS.
	 
	 <NFS server> --> hostname or IP address of the NFS server.

	 <remote directory> --> the path to the shared directory on the NFS server.

	<local directory>` --> the path to the desired mount point on the client system.

	-nolock --> Specifies not to use NLM locking

**Nlm locking** - 
In simple terms, NLM locking ensures that only one client can modify a file at a time, while multiple clients can read the file simultaneously without interfering with each other.



#### Listing NFS shares on remote server:
```python
root@ip-10-10-0-197:~# /usr/sbin/showmount -e 10.10.36.100
Export list for 10.10.36.100:
/home *
```

	/usr/sbin/showmount --> location of remote share

	10.10.36.100 --> IP of remote server

