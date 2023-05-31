- this command allows you to transfer files between two computers using the SSH protocol to provide both authentication and encryption.
- SCP allows you to:
	- Copy files & directories from your current system to a remote system
	- Copy files & directories from a remote system to your current system
- Provided that we know usernames and passwords for a user on your current system and a user on the remote system

## Example 
1. For example, let's copy an example file from our machine to a remote machine

```bash
scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt
```

![[scp_example1.png]]

2. using `scp` to copy a file from a remote computer that we're not logged into
```bash
scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt
```
![[scp_example2.png]]


