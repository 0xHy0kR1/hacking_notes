## Introduction 
- There are multiple ways to set up an HTTP web serveri in Kali linux. Apache, NGINX, and python are a few of the ways this can be accomplished.
- Python is the quickest among them. 

# Prerequisite - Python 3, Apache, NGINX, installed on your system depends on which web server you want to host.

## Installing python 3
```python
┌──(hyok㉿kali)-[~]
└─$ sudo apt install python3 
```

## Installing apache 2
```python
┌──(hyok㉿kali)-[~]
└─$ sudo apt install apache2
```

## Installing NGINX 
```python
┌──(hyok㉿kali)-[~]
└─$ sudo apt install nginx
```

## Lets try now here with python 3
- Python SimpleHTTPServer module is a very handy tool. 
- You can use Python SimpleHTTPServer to turn any directory into a simple HTTP web server. 
- Python SimpleHTTPServer supports only two HTTP methods - GET and HEAD.
- Python SimpleHTTPServer has been migrated to python `http.server` module in python 3.
- If you are using linux operating system then go to your desired folder or directory that you want to share.
- You can run python http server on any port, default port is 8000.
- To start server, type below one's.
```python 
┌──(hyok㉿kali)-[/opt/unicorn/hta_attack]
└─$ python3 -m http.server --bind 192.168.1.7 9000 
```

- For help purpose, type as follows;
```python
┌──(hyok㉿kali)-[/opt/unicorn/hta_attack]
└─$ python3 -m http.server -h
usage: server.py [-h] [--cgi] [-b ADDRESS] [-d DIRECTORY] [-p VERSION] [port]

positional arguments:
  port                  bind to this port (default: 8000)

options:
  -h, --help            show this help message and exit
  --cgi                 run as CGI server
  -b ADDRESS, --bind ADDRESS
                        bind to this address (default: all interfaces)
  -d DIRECTORY, --directory DIRECTORY
                        serve this directory (default: current directory)
  -p VERSION, --protocol VERSION
                        conform to this HTTP version (default: HTTP/1.0)
```

