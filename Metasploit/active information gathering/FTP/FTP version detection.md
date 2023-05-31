- The scanner/ftp/ftp_version module is a scanner that is used to identify the version of the FTP server that is running on a remote system.
- The module works by connecting to the target FTP server and sending a series of probes to identify the version of the FTP software that is running.
# Code - 
```python
msf6 auxiliary(scanner/ssh/ssh_login) > use auxiliary/scanner/ftp/ftp_version
msf6 auxiliary(scanner/ftp/ftp_version) > set RHOSTS 192.168.216.11
RHOSTS => 192.168.216.11
msf6 auxiliary(scanner/ftp/ftp_version) > set THREADS 256
THREADS => 256
msf6 auxiliary(scanner/ftp/ftp_version) > run

[+] 192.168.216.11:21     - FTP Banner: '220 Microsoft FTP Service\x0d\x0a'
[*] 192.168.216.11:21     - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed```

# Some extra information - 
- The scan results, as with the previous auxiliary modules, will get stored in the Metasploit database and can be accessed using the services command:
```python
msf6 auxiliary(scanner/ftp/ftp_version) > services
Services
========

host            port   proto  name          state  info
----            ----   -----  ----          -----  ----
192.168.216.4   53     udp    dns           open   BIND 9.4.2
192.168.216.4   111    tcp    sunrpc        open   100000 v2
192.168.216.4   111    udp    portmap       open   100000 v2 TCP(111), 100000 v2 UDP(111), 100024 v1 UDP(54265), 100024 v1 TCP(55287),
                                                    100003 v2 UDP(2049), 100003 v3 UDP(2049), 100003 v4 UDP(2049), 100021 v1 UDP(58592
                                                   ), 100021 v3 UDP(58592), 100021 v4 UDP(58592), 100003 v2 TCP(2049), 100003 v3 TCP(2
                                                   049), 100003 v4 TCP(2049), 100021 v1 TCP(33417), 100021 v3 TCP(33417), 100021 v4 TC
                                                   P(33417), 100005 v1 UDP(47926), 100005 v1 TCP(37458), 100005 v2 UDP(47926), 100005
                                                   v2 TCP(37458), 100005 v3 UDP(47926), 100005 v3 TCP(37458)
192.168.216.4   137    udp    netbios       open   METASPLOITABLE:<00>:U :METASPLOITABLE:<03>:U :METASPLOITABLE:<20>:U :WORKGROUP:<00>
                                                   :G :WORKGROUP:<1e>:G :00:00:00:00:00:00
192.168.216.4   2049   tcp    sunrpc        open   100003 v4
192.168.216.4   2049   udp    sunrpc        open   100003 v4
192.168.216.4   33417  tcp    sunrpc        open   100021 v4
192.168.216.4   37458  tcp    sunrpc        open   100005 v3
192.168.216.4   47926  udp    sunrpc        open   100005 v3
192.168.216.4   54265  udp    sunrpc        open   100024 v1
192.168.216.4   55287  tcp    sunrpc        open   100024 v1
192.168.216.4   58592  udp    sunrpc        open   100021 v4
192.168.216.7   22     tcp    ssh           open   OpenSSH 7.1 protocol 2.0
192.168.216.7   135    tcp    msrpc         open   Microsoft Windows RPC
192.168.216.7   445    tcp    microsoft-ds  open   Windows Server 2008 R2 Standard 7601 Service Pack 1 microsoft-ds
192.168.216.7   49153  tcp    msrpc         open   Microsoft Windows RPC
192.168.216.7   49154  tcp    msrpc         open   Microsoft Windows RPC
192.168.216.9   22     tcp    ssh           open   SSH-2.0-OpenSSH_9.2p1 Debian-2
192.168.216.10  135    tcp    msrpc         open   Microsoft Windows RPC
192.168.216.10  139    tcp    netbios-ssn   open   Microsoft Windows netbios-ssn
192.168.216.10  445    tcp    microsoft-ds  open   Windows 7 Home Premium 7601 Service Pack 1 microsoft-ds workgroup: WORKGROUP
192.168.216.10  554    tcp    rtsp          open
192.168.216.10  2869   tcp    http          open   Microsoft HTTPAPI httpd 2.0 SSDP/UPnP
192.168.216.10  5357   tcp    http          open   Microsoft HTTPAPI httpd 2.0 SSDP/UPnP
192.168.216.10  10243  tcp    http          open   Microsoft HTTPAPI httpd 2.0 SSDP/UPnP
192.168.216.10  49152  tcp    msrpc         open   Microsoft Windows RPC
192.168.216.10  49153  tcp    msrpc         open   Microsoft Windows RPC
192.168.216.10  49154  tcp    msrpc         open   Microsoft Windows RPC
192.168.216.10  49155  tcp    msrpc         open   Microsoft Windows RPC
192.168.216.10  49156  tcp    msrpc         open   Microsoft Windows RPC
192.168.216.10  49158  tcp    msrpc         open   Microsoft Windows RPC
192.168.216.11  21     tcp    ftp           open   220 Microsoft FTP Service\x0d\x0a
192.168.216.11  22     tcp    ssh           open   SSH-2.0-OpenSSH_7.1
192.168.216.11  445    tcp    smb           open   SMB Detected (versions:1, 2) (preferred dialect:SMB 2.1) (signatures:optional) (upt
                                                   ime:40m 6s) (guid:{d82b1a6d-b657-4a62-b4b2-39511412b4da}) (authentication domain:VA
                                                   GRANT-2008R2)Windows 2008 R2 Standard SP1 (build:7601) (name:VAGRANT-2008R2) (workg
                                                   roup:WORKGROUP)

```
