## 1. To set up our Metasploit database, we first need to start up the PostgreSQL server, using the following command:
```python
root@kali:~# systemctl start postgresql
```

## 2. Then we need to create and initialize the msf database with the msfdb command with the init option:
```python
root@kali:~# msfdb init
```

## 3. To display all the msfdb options, run the command as follows:
```python
root@kali:~# msfdb
```

## 4. To modify the database configuration file, we can edit the database.yml file located in /usr/share/metasploit-framework/config/database.yml:
```python
root@kali:~# cat /usr/share/metasploitframework/config/database.yml
```

## 5. Now, let's launch the msfconsole interface and confirm that Metasploit is successfully connected to the database using the db_status command:
```python
msf > db_status
```

