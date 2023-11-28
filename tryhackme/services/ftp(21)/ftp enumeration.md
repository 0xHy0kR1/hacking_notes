## Pre-requisite --> [[tryhackme/services/enumeration]]
## ftp anonymous login
As we're going to be logging in to an FTP server, we will need to make sure an FTP client is installed on the system, confirm it by typing "ftp" in the console.

1. First scan with nmap to check if there is a anonymous login supported or not:
   ![[ftp1.png]]

2. Try login with Anonymous username(or whatever username you find during recon) and press ENTER when prompting for password:
   ![[ftp2.png]]
   