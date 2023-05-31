- The services command allows us to display the services running on the hosts
# 1. To view the help for the services command, we can use the -h option:
```python
msf > services -h
```

# 2. Using the "services" command without any options displays all the available services:
```python
msf > services
```

# 3. Searching for specific service using service command: 
```python
msf > services -S ssh
```

# 4. Search for a port number as follows: 
```python
msf > services -p 22
```

# 5. By combining multiple options, you can search just a specific host and only display the columns you want:
```python
services -c name,port,info -S  ssh 192.168.216.10
```
