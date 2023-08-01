1. Installing gobuster
```python
sudo apt install gobuster
```

![[web_enum1.png]]

**Directory listing** - 
- It is the listing of files in the directory that we are navigating to(just as if we were to use Windows Explorer or Linux's `ls` command.)
- "Directory Listing" occurs when there is no file present that the webserver has been told to process.
- A very common file is "index.html" and "index.php". As these files aren't present in /a/directory, the contents are instead displayed:
![[web_enum8.png]]

## Gobuster modes
1. dir mode
	- It has a "dir" mode that allows the user to enumerate website directories.
	- Gobuster is powerful because it not only allows you to scan the website, but it will return the status codes as well.
	- To use "dir" mode, you start by typing `gobuster dir`.
```python
gobuster dir -u http://10.10.10.10 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 50
```

### Other Useful Flags
These are common flags.
![[web_enum2.png]]
- A very common use of Gobuster's "dir" mode is the ability to use it's `-x` or `--extensions` flag to search for the contents of directories that you have already enumerated by providing a list of file extensions.
- For example, **.conf** or **.config** files usually contain configurations for the application - including sensitive info such as database credentials.

**search the "myfolder" directory on a webserver for the following three files:**
1. html
2. js
3. css
```python
gobuster dir -u http://10.10.252.123/myfolder -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x.html,.css,.js -t 50
```  

1. The -k Flag
- if HTTPS is enabled, you will most likely encounter an invalid cert error like the one below.
![[web_enum3.png]]
- if you try to run Gobuster against this without the `-k` flag, then it just return the above error.
Note: This flag can be used with "dir" mode and "vhost" modes

### dns Mode
- This allows Gobuster to brute-force subdomains.
- Just because something is patched in the regular domain, does not mean it is patched in the sub-domain.
- To use "dns" mode, you start by typing `gobuster dns`.
- After that, you will need to add the domain and wordlist using the -d and -w options, respectively. Like so:
```python
gobuster dns -d mydomain.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -t 50
```

### Other Useful Flags
- -d and -w are the main flags that you'll need for _most_ of your scans.
![[web_enum4.png]]

### vhost Mode
- This allows Gobuster to brute-force virtual hosts.
- Virtual hosts are different websites on the same machine.
- In some instances, they can appear to look like sub-domains, but don't be deceived! Virtual Hosts are IP based and are running on the same server.
- To use "vhost" mode, you start by typing `gobuster vhost`.
- After that, you will need to add the domain and wordlist using the `-u` and `-w` options, respectively. Like so:
```python
gobuster vhost -u http://example.com -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain -t 50
```

**NOTE** - 
1. For find any files in the VHOST you should first add them on your /etc/hosts with the corresponding ip.
