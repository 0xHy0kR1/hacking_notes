## Introduction 
- Also known as Directory traversal, a web security vulnerability allows an attacker to read operating system resources, such as local files on the server running an application.
- The attacker exploits this vulnerability by manipulating and abusing the web application's URL to locate and access files or directories stored outside the application's root directory.

## Why the path traversal vulnerability happen?
- Path traversal vulnerabilities occur when the user's input is passed to a function such as file_get_contents in PHP.
- It's important to note that the function is not the main contributor to the vulnerability. Often poor input validation or filtering is the cause of the vulnerability

**The following graph shows how a web application stores files in /var/www/app**
![[file_inclusion3.png]]
- Path traversal attacks, also known as the dot-dot-slash attack, take advantage of moving the directory one step up using the double dots ../
- If the attacker finds the entry point, which in this case get.php?file=, then the attacker may send something as follows, http://webapp.thm/get.php?file=../../../../etc/passwd.

- Each .. entry moves one directory until it reaches the root directory /. Then it changes the directory to /etc, and from there, it read the passwd file.
![[file_inclusion4.png]]
As a result, the web application sends back the file's content to the user.
![[file_inclusion5.png]]

**Note** - Similarly, if the web application runs on a Windows server, the attacker needs to provide Windows paths.

### Example
if the attacker wants to read the boot.ini file located in c:\boot.ini, then the attacker can try the following depending on the target OS version:

```bash
http://webapp.thm/get.php?file=../../../../boot.ini 
						or
http://webapp.thm/get.php?file=../../../../windows/win.ini
```

## Below are some common OS files you could use when testing.
![[file_inclusion6.png]]