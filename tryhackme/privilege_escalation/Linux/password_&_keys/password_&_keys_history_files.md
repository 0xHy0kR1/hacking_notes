If a user accidentally types their password on the command line instead of into a password prompt, it may get recorded in a history file.

**View the contents of all the hidden history files in the user's home directory:**
```python
cat ~/.*history | less
```
- Note that the user has tried to connect to a MySQL server at some point, using the "root" username and a password submitted via the command line.
- Note that there is no space between the -p option and the password!

**Switch to the root user, using the password:**
```python
su root
```

## Practically - 
### In target machine - 
![[linux_privesc23.png]]

**Contents of history file** - 
![[linux_privesc24.png]]
