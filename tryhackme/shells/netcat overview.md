## Introduction

#### Reverse Shells
**The syntax for starting a netcat listener using Linux is this:**

```python
nc -lvnp <port-number>
```
- **-l** is used to tell netcat that this will be a listener
- **-v** is used to request a verbose output
- **-n** tells netcat not to resolve host names or use DNS.
- **-p** indicates that the port specification will follow.
**Note** - if you choose to use a port below 1024, you will need to use `sudo` when starting your listener. it's often a good idea to use a well-known port number (80, 443 or 53 being good choices) as this is more likely to get past outbound firewall rules on the target.

**Working example** - 
```python
sudo nc -lvnp 443`
```

#### Bind Shells
**The syntax for this is relatively straight forward:**

```python
nc <target-ip> <chosen-port>
```

