## Dirb
It is used to find hidden files and directories within a web server.
A **path traversal** attack is also known as “_directory traversal”_ aims to access files and directories that are stored outside the web root folder.
It is a content scanner, not a vulnerability scanner.

### Utilizing Multiple Wordlist for Directory Traversing
```python
┌──(hyok㉿kali)-[~]
└─$ ls /usr/share/wordlists/dirb
big.txt  catala.txt  common.txt  euskera.txt  extensions_common.txt  indexes.txt  mutations_common.txt  others  small.txt  spanish.txt  stress  vulns
```

### Default working of Dirb
In this attack, the common.txt is set as a default word list for directory traversal.
```python
┌──(hyok㉿kali)-[~]
└─$ dirb http://192.168.1.7 /usr/share/wordlists/dirb/common.txt
```

### Enumerating Directory with Specific Extension List
The -X parameter accepts the file extension name and then searches the given extension files over the target server or machine.
```python
┌──(hyok㉿kali)-[~]
└─$ dirb http://192.168.1.7 -X .php                             
```

### Save Output to Disk
we will use the parameter -o of the dirb scan we can save the output of the dirb scan in a text file.
```python
┌──(hyok㉿kali)-[~]
└─$ dirb http://192.168.1.7 -o output.txt
```
In the above case the location of output.txt is the current folder(~)

### Ignore Unnecessary Status-Code
we are using –N parameter on code 302 to ignore it.
```python
┌──(hyok㉿kali)-[~]
└─$ dirb http://192.168.1.7/ -N 403      
```

### Avoiding warning messages and do in-depth scan
```python
┌──(hyok㉿kali)-[~]
└─$ dirb http://192.168.1.7/ -w 
```

### Speed delay
- While working in different scenarios, there is some environment we come across that cannot handle the flood created by the dirb scan, so in those environments, it is important that we delay the scan for some time
- the time is provided on the scale of milliseconds.
```python
┌──(hyok㉿kali)-[~]
└─$ dirb http://192.168.1.7/ -z 100
```

### Not recursively
- The dirb scan, by default, scans the directories recursively. It means it scans a directory and then traverses inside that directory to scan for more subdirectories.
- But in some scenarios, where time is insufficient, we set the dirb to not scan recursively. This can be achieved using the **-r parameter**.

```python
┌──(hyok㉿kali)-[~]
└─$ dirb http://192.168.1.7/ -r
```

### Show Not existence pages
In some scenarios we need to find the 404 pages too, which dirb skips by default. To find those pages we will use -v parameter.
```python
┌──(hyok㉿kali)-[~]
└─$ dirb http://192.168.1.7/ -v
```

### Extension Header(-H)
by using **–H parameter** with specific extension, for example .php along with target URL it will enumerate all files or directories named with php as shown in the given below image.
```python
┌──(hyok㉿kali)-[~]
└─$ dirb http://192.168.1.7/ -H .php
```