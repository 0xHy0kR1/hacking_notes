- The gather/shodan search module is a tool that allows you to use the Shodan API to search for information about devices and systems that are connected to the internet.
- Shodan is also a useful tool for identifying the location of your target and checking if it has any internet-facing devices.
- . Shodan lets you search for banners, grabs metadata about the device, such as its geographic location, hostname, operating system, and more.
```python
msf6 auxiliary(gather/censys_search) > use auxiliary/gather/shodan_search
msf6 auxiliary(gather/shodan_search) > set SHODAN_APIKEY w5qcXhi65isv2CqiHHFkpF77Vdg5maxc
SHODAN_APIKEY => w5qcXhi65isv2CqiHHFkpF77Vdg5maxc
msf6 auxiliary(gather/shodan_search) > run

[*] Total: 4 on 1 pages. Showing: 1 page(s)
[*] Collecting data, please wait...

Search Results
==============

 IP:Port             City    Country  Hostname
 -------             ----    -------  --------
 52.213.144.44:443   Dublin  Ireland  ec2-52-213-144-44.eu-west-1.compute.amazonaws.com
 54.194.159.236:443  Dublin  Ireland  packt.com
 54.73.56.161:443    Dublin  Ireland  packt.com
 99.81.64.155:443    Dublin  Ireland  packt.com

[*] Auxiliary module execution completed
```
## Some extra information - 
- The Shodan Search auxiliary module has revealed further information about the target, such as its IP address, open ports, location, and so on.