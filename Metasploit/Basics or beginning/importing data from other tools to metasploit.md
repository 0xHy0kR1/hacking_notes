# Example - To test the db_import command, we will use the nmap command.
## 1. Here is the syntax used to scan the Metasploitable 3 target machine:
```python
nmap -Pn -A -oX report 192.168.216.10
```

## 2. To import the scan report, you can use the db_import command followed by the path to the report you want to import:
```python
msf > db_import /root/report
```

## Some extra info - 
### The db_nmap command works the same way as the regular nmap command:
```python
msf > db_nmap -Pn -A 192.168.216.129
```
