## 1. Issuing the hosts command with -h will display the help menu:
```python
msf > hosts -h
```

## 2.  Using the -c option, we can select which columns to display:
```python
msf > hosts -c address,os_name 
```

## 3. With the -S option, we can search for specific strings, such as the OS name:
```python
msf > hosts -c address,os_name
```
