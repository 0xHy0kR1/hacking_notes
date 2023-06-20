## Pre-requisite --> [[enumeration]]
SMB can often be a great starting point for an attacker looking to discover sensitive information

## Enumerating SMB shares with Enum4Linux:
-  Enum4linux is a tool used to enumerate SMB shares on both Windows and Linux systems.
-  it easy to quickly extract information from the target.

### Syntax
```python
enum4linux [options] ip
```
**TAG**            **FUNCTION**  

-U             get userlist  
-M             get machine list  
-N             get namelist dump (different from -U and-M)  
-S             get sharelist  
-P             get password policy information  
-G             get group and member list

-a             all of the above (full basic enumeration)

### Example
```python
enum4linux -a 192.168.1.13
```