## To display the help menu, simply type the help command inside msfconsole:
```python
msf > help
```

## "search" command to search anything in the database:
```python
msf > search -h
```

## Auxiliary
Any supporting module, such as scanners, crawlers and fuzzers, can be found here.
![[ms1.png]]

## Encoders
- Encoders will allow you to encode the exploit and payload in the hope that a signature-based antivirus solution may miss them.
- Signature-based antivirus and security solutions have a database of known threats. They detect threats by comparing suspicious files to this database and raise an alert if there is a match.
- Thus encoders can have a limited success rate as antivirus solutions can perform additional checks.
![[ms2.png]]

## Exploits
![[ms3.png]]

## NOPs
- NOPs (No OPeration) do nothing, literally.
- They are often used as a buffer to achieve consistent payload sizes.
![[ms4.png]]

## Payloads
Payloads are codes that will run on the target system.
![[ms5.png]]

#### You will see four different directories under payloads: adapters, singles, stagers and stages:
###### Adapters:
- An adapter wraps single payloads to convert them into different formats.
	- For example, a normal single payload can be wrapped inside a Powershell adapter, which will make a single powershell command that will execute the payload.

###### Singles:
- Self-contained payloads (add user, launch notepad.exe, etc.) that do not need to download an additional component to run.

###### Stagers:
- Responsible for setting up a connection channel between Metasploit and the target system.
- Useful when working with staged payloads. “Staged payloads” will first upload a stager on the target system then download the rest of the payload (stage).
- This provides some advantages as the initial size of the payload will be relatively small compared to the full payload sent at once.

###### Stages: 
- Downloaded by the stager. This will allow you to use larger sized payloads.
Example - 
- generic/shell_reverse_tcp
- windows/x64/shell/reverse_tcp

The former is an inline (or single) payload, as indicated by the “_” between “shell” and “reverse”. While the latter is a staged payload, as indicated by the “/” between “shell” and “reverse”.

## Post
Post modules will be useful on the final stage of the penetration testing process
![[ms6.png]]

## Regular commands used in metasploit
1. `ls`
2. `clear`
3. It doesn't support output redirection
4. `help (command)`
5. `history`

## Example of an exploit settings and use
1. type the `use exploit/windows/smb/ms17_010_eternalblue` command
2. The module to be used can also be selected with the `use` command followed by the number at the beginning of the search result line.
![[ms7.png]]

3. The prompt tells us we now have a context set in which we will work. You can see this by typing the show options command.
![[ms8.png]]

4. The `show` command can be used in any context followed by a module type (auxiliary, payload, exploit, etc.) to list available modules. The example below lists payloads that can be used with the ms17-010 Eternalblue exploit.
![[ms9.png]]

5. You can leave the context using the `back` command.
![[ms10.png]]

6. Further information on any module can be obtained by typing the `info` command within its context. Info is not a help menu; it will display detailed information on the module such as its author, relevant sources, etc.
![[ms11.png]]
-----------------------------SNIP-----------------------------------------------

7. `search` command will search the Metasploit Framework database for modules relevant to the given search parameter. You can conduct searches using CVE numbers, exploit names (eternalblue, heartbleed, etc.), or target system.
![[ms12.png]]

8. Module ranking
![[ms13.png]]

9. You can direct the search function using keywords such as type and platform.
For example, if we wanted our search results to only include auxiliary modules, we could set the type to auxiliary.
![[ms14.png]]

**Note** - Please remember that exploits take advantage of a vulnerability on the target system and may always show unexpected behavior. A low-ranking exploit may work perfectly, and an excellent ranked exploit may not, or worse, crash the target system.

