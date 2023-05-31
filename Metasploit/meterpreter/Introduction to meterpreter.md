- what we can do after we have exploited the target machine. Meterpreter provides us with many features that can ease our task of exploring the target machine.
- Meterpreter is a post-exploitation tool that is commonly used in penetration testing and ethical hacking to gain remote access to a compromised system.
## Why we can't use payload instead of meterpreter
- We have been using payloads in order to achieve specific results, but they have a major disadvantage.
- Payloads work by creating new processes in the compromised system. This can trigger alarms in antivirus programs and can be caught easily. Also, a payload is limited to perform only some specific tasks or execute specific commands that the shell can run. To overcome these difficulties, Meterpreter was created.
- When Meterpreter is used, it injects itself into a running process on the compromised system, typically a legitimate process such as explorer.exe or svchost.exe. This allows Meterpreter to run in memory without creating a new process that could be detected by antivirus software or other security measures.
- In contrast, when a payload is used to exploit a vulnerability, it typically creates a new process on the compromised system. This can be detected by security software and is generally less stealthy than using Meterpreter.
- Meterpreter uses encrypted communication with the target, which is another major advantage of using it.

## Stepwise representation of loading meterpreter:
							![[Stepwise_img_of_loading_meterpreter.jpeg]]
- In the first step, the exploit and first stage payload are sent to the target machine.
- After the exploitation, the stage establishes a TCP connection back to `msfconsole` on a given address and port.
- Next, `msfconsole` sends the second stage DLL injection payload.
- After successful injection, it sends the meterpreter DLL to establish a proper commucation channel.
- Lastly, Meterpreter loads extensions such as stdapi and priv. All these extensions are loaded over [[TLS]] using a [[TLV]] protocol.

## Advantages of Meterpreter
- It can migrate easily among process.
- It resides completely in memory, so it writes nothing to disk.
- It uses encrypted communications.
- It uses a channelized communication system so that we can work with several channels at a time.
- It provides a platform to write extensions quickly and easily.

