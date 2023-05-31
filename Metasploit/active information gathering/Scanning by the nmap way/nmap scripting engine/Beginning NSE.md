- The Nmap Scripting Engine (NSE) is a powerful feature of Nmap that allows users to write and execute custom scripts to automate tasks, gather more detailed information about a target, and perform more advanced scans.
- The NSE scripts are written in the Lua programming language.
# The NSE scripts can be used to perform a variety of tasks, such as:
1.  Detecting vulnerable services and applications on a network
2.  Gathering information about remote hosts and services
3.  Performing DNS queries and zone transfers
4.  Conducting brute-force attacks against login systems and web applications
5.  Testing the security of web applications by looking for common vulnerabilities such as SQL injection and cross-site scripting (XSS)
# Code - 
#### The basic syntax for running the NSE scripts is as follows:
```python
nmap --script <scriptname> <host ip>
```

#### The same applies to the db_nmap command, so let's use the NSE to try to find some HTTP/HTTPS vulnerabilities:
```python
msf > db_nmap --open -sTV -Pn -p 80,443,8000,8080,8585 --script=httpvhosts,http-userdir-enum,http-apache-negotiation,http-backup-finder,httpconfig-backup,http-default-accounts,http-methods,http-method-tamper,httppasswd,http-robots.txt,ssl-poodle,ssl-heartbleed,http-webdav-scan,http-iiswebdav-vuln 192.168.216.1
```
