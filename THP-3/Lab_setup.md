## Setting up VPS on amazon
1. Visit --> https://lightsail.aws.amazon.com/ 
2. Create an Instance 
	- I highly recommend getting at least 1 GB of RAM 
	- Storage space usually isn't an issue 
3. Linux/Unix 
4. OS Only -> Ubuntu 
5. Download Cert
6. chmod 600 cert 
7. ssh -i cert ubuntu@(ip)

#### Download all the tools in server
Once you are logged into your server, you need to install all the tools as efficiently and repeatable as possible. This is where I recommend that you develop your own scripts to set up things such as IPTables rules, SSL certs, tools, scripts, and more. A quick way to build your servers is to integrate TrustedSec's The PenTesters Framework (PTF). This collection of scripts (https://github.com/trustedsec/ptf) does a lot of the hard work for you and creates a framework for everything else.

After cloning the above repo into your server then you should go through below steps:
1. sudo su - 
2. apt-get update 
3. apt-get install python 
4. git clone https://github.com/trustedsec/ptf /opt/ptf 
5. cd /opt/ptf && ./ptf 
6. use modules/exploitation/install_update_all 
7. use modules/intelligence-gathering/install_update_all 
8. use modules/post-exploitation/install_update_all 
9. use modules/powershell/install_update_all 
10. use modules/vulnerability-analysis/install_update_all 
11. cd /pentest