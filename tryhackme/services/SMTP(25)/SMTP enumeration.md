## Pre-requisite --> [[tryhackme/services/enumeration]]

## Enumerating server details:
We're going to use the "_smtp_version_" module in MetaSploit, it will scan a range of IP addresses and determine the version of any mail servers it encounters.

## Enumerating Users from SMTP
**Commands to enumerate users**:
- VRFY (confirming the names of valid users)
- EXPN (which reveals the actual address of user’s aliases and lists of e-mail (mailing lists).
Using these SMTP commands, we can reveal a list of valid users.

**Note** - 1
- enumeration can be done with telnet connection - however metasploit module "smtp_enum" is a great way to do this.
- There are alternatives to metasploit and which is **smtp-user-enum** for OSCP PREP.
- Enumeration is performed by inspecting the responses to VRFY, EXPN, and RCPT TO commands.

## SMTP enumeration practically:

**finding the version info of SMTP with metasploit**:
```python
msf6 > use scanner/smtp/smtp_version
msf6 > set RHOSTS 10.10.92.67
msf6 > run
```
![[SMTP2.png]]

**enumerating users on SMTP**:
```python
msf6 > use auxiliary/scanner/smtp/smtp_enum
msf6 > set RHOSTS 10.10.92.67
msf6 auxiliary(scanner/smtp/smtp_enum) > set USER_FILE /usr/share/wordlists/SecLists/Usernames/top-usernames-shortlist.txt
```
![[SMTP3.png]]