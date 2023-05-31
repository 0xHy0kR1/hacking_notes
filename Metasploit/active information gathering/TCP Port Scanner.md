# Pre-reuisite - [[Configuring the PostgreSQL database for metasploit]]
# pre-requisite - [[Active information gathering]]
- We can start by doing a basic TCP portscan with the TCP Port Scanner auxiliary module and see what we can find.
- the TCP Port Scanner auxiliary module does not need administrative privileges on the source machine.
# Code - 
```python
msf6 > use auxiliary/scanner/portscan/tcp
msf6 auxiliary(scanner/portscan/tcp) > set RHOSTS 192.168.216.0/24
RHOSTS => 192.168.216.0/24
msf6 auxiliary(scanner/portscan/tcp) > set THREADS 100
THREADS => 100
msf6 auxiliary(scanner/portscan/tcp) > run

[+] 192.168.216.3:        - 192.168.216.3:1 - TCP OPEN
[+] 192.168.216.3:        - 192.168.216.3:6 - TCP OPEN
[+] 192.168.216.3:        - 192.168.216.3:8 - TCP OPEN
[+] 192.168.216.4:        - 192.168.216.4:22 - TCP OPEN
[+] 192.168.216.3:        - 192.168.216.3:12 - TCP OPEN
[+] 192.168.216.9:        - 192.168.216.9:22 - TCP OPEN
[+] 192.168.216.4:        - 192.168.216.4:23 - TCP OPEN
[+] 192.168.216.3:        - 192.168.216.3:21 - TCP OPEN
---------------SNIP-------------------------
[*] Auxiliary module execution completed
```
# Some Extra information - 
- When using Metasploit modules, you can check the available options for that specific module using the show options command.
- Use the show missing command to show the missing values required by the module.
- Scanners and most other auxiliary modules use the ‘RHOSTS’ option instead of ‘RHOST’.
- RHOSTS can take IP ranges (192.168.1.20-192.168.1.30), CIDR ranges (192.168.1.0/24), multiple ranges separated by commas (192.168.1.0/24, 192.168.3.0/24), and line-separated host list files (file:/tmp/hostlist.txt).
- By default, all of the scanner modules will have the ‘THREADS’ value set to ‘1’.
- The ‘THREADS’ value sets the number of concurrent threads to use while scanning.
- Set this value to a higher number in order to speed up your scans or keep it lower in order to reduce network traffic but be sure to adhere to the following guidelines:
	-   Keep the THREADS value under 16 on native Win32 systems
	-   Keep THREADS under 200 when running MSF under Cygwin
	-   On Unix-like operating systems, THREADS can be set as high as 256.