## Introduction
- It is a very popular vulnerability scanner due to being both open-source nature and feature-rich.
- Nikto can be used to discover possible vulnerabilities including:
	- Sensitive files
	- Outdated servers and programs (i.e. vulnerable web server installs)
	- Common server and software misconfigurations (Directory indexing, cgi scripts, x-ss protections)

## Installing nikto
```python
sudo apt update && sudo apt install nikto
```

## Nikto modes 

### Basic scanning
- The most basic scan can be performed by using the -h flag and providing an IP address or domain name as an argument.
- This scan type will retrieve the headers advertised by the webserver or application (I.e. Apache2, Apache Tomcat, Jenkins or JBoss).
- It will also look for any sensitive files or directories (i.e. login.php, /admin/, etc).
```python
nikto -h vulnerable_ip
```
![[web_enum11.png]]

**Note a few interesting things are given to us in this example:**
- Nikto has identified that the application is Apache Tomcat using the favicon and the presence of "_/examples/servlets/index.html_" which is the location for the default Apache Tomcat application.
- HTTP Methods "_PUT_" and "_DELETE_" can be performed by clients - we may be able to leverage these to exploit the application by uploading or deleting files.

### Scanning Multiple Hosts & Ports
We must instruct Nmap to output a scan into a format that is friendly for Nikto to read using Nmap's  `-oG`  flags.
**Example** - 
we can scan 172.16.0.0/24 (subnet mask 255.255.255.0, resulting in 254 possible hosts) with Nmap (using the default web port of 80) and parse the output to Nikto like so:
```python
nikto -h 10.10.10.1 -p 80,8000,8080
```

**scanning multiple ports on one specific host** - 
- We can do this by using the `-p` flag and providing a list of port numbers delimited by a comma.
```python
nikto -h 10.10.10.1 -p 80,8000,8080
```

### Introduction to Plugins
- Using information gathered from our basic scans, we can pick and choose plugins that are appropriate to our target.
- You can use the `--list-plugins` flag with Nikto to list the plugins(For online go [here](https://github.com/sullo/nikto/wiki/Plugin-list))
**Some interesting plugins include:**
![[web_enum12.png]]
- We can specify the plugin we wish to use by using the `-Plugin` argument and the name of the plugin we wish to use.
**Example** - 
```python
nikto -h 10.10.10.1 -Plugin apacheuser
```

### Verbosing our Scan 
- We can increase the verbosity of our Nikto scan by providing the following arguments with the `-Display` flag.
- Unless specified, the output given by Nikto is not the entire output, as it can sometimes be irrelevant (but that isn't always the case!).
![[web_enum13.png]]

### Tuning Your Scan for Vulnerability Searching
We can use the `-Tuning` flag and provide a value in our Nikto scan:
![[web_enum14.png]]

### Saving Your Findings
Nikto is capable of putting output to a few file formats including:
	-  Text File
	-  HTML report
- We can use the `-o` argument (short for `-Output`) and provide both a filename and compatible extension.
- We _can_ specify the format (`-f`) specifically, but Nikto is smart enough to use the extension we provide in the `-o` argument to adjust the output accordingly.
**Example** - 
```python
nikto -h http://ip_address -o report.html
```

