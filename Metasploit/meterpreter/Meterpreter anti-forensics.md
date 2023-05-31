# Pre-requisite - [[Modified-Accessed-Created-Entry]]
- Why change the MACE values? Hackers generally use the technique of changing the MACE values to make the target user think that the file has been present on the system for a long time and that it has not been touched or modified.
- In case of suspicious activity, the administrators may check for recently modified files to find out whether any of the files have been modified or accessed. So, using this technique, the file will not appear in the list of recently accessed or modified items

## Listing the values of MACE of file:
```python
meterpreter > timestomp C:\\test.txt -v
[*] Showing MACE attributes for C:\test.txt
Modified      : 2023-03-15 15:54:02 +0530
Accessed      : 2023-03-15 15:54:02 +0530
Created       : 2023-03-15 15:54:02 +0530
Entry Modified: 2023-03-15 15:54:05 +0530
```

## Changing the creation time of the file 
```python
meterpreter > timestomp C:\\test.txt -c "10/25/2050 01:01:01"
[*] Setting specific MACE attributes on C:\test.txt
```

## Changing the modified time of the file
```python
meterpreter > timestomp C:\\test.txt -m "1/1/2051 01:00:00"
[*] Setting specific MACE attributes on C:\test.txt
```

## Changing the accessed time of the file
```python
meterpreter > timestomp C:\\test.txt -a "1/1/2005 02:00:01"
[*] Setting specific MACE attributes on C:\test.txt
```

Note - Alternatively, we can also use the -z operator to change all four MACE values in one go but it assign the same values to all four MACE attributes.