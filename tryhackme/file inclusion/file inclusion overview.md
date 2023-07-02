### The following diagram breaks down the essential parts of a URL.
![[file_inclusion1.png]]

For example, if a user wants to access and display their CV within the web application, the request may look as follows, http://webapp.thm/get.php?file=userCV.pdf, where the file is the parameter and the userCV.pdf, is the required file to access.
![[file_inclusion2.png]]

## Why do File inclusion vulnerabilities happen?
- File inclusion vulnerabilities are commonly found and exploited in various programming languages for web applications, such as PHP.
- The main issue of these vulnerabilities is the input validation, in which the user inputs are not sanitized or validated, and the user controls them. When the input is not validated, the user can pass any input to the function, causing the vulnerability.

## What is the risk of File inclusion?
- By default, an attacker can leverage file inclusion vulnerabilities to leak data, such as code, credentials or other important files related to the web application or operating system