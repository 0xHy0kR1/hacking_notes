- Adding a malicious code to a software application that is already known to the target, which can be a good way to gain unauthorized access to the target's system.
- For example, if an attacker has access to the target's internal network, they may be able to compromise the target's [[software repository]] and add their own malicious code to a commonly used application.
- Using a "custom template" can help an attacker bypass security solutions that are designed to detect Metasploit payloads.
- Security solutions often use default templates to detect these payloads, but by using a customized template, the attacker may be able to avoid detection and successfully execute their malicious code.
## Where the metasploit templates stored?
- MSFvenom, by default, uses the templates in the `/usr/share/metasploit-framework/data/templates` 
- We can choose to use our own, using the `-x` option.

## Some information
- The hacker can use a tool called "Process Explorer" to launch their payload on the target system.
- Process Explorer is a legitimate tool developed by Microsoft Sysinternals that allows users to see detailed information about running processes on a Windows system.
- By using the "-x" option, the hacker can specify their own custom template for Process Explorer to use. This template will include their payload code.
- Using the "-k" option, the hacker can run their payload code as a new thread within the Process Explorer process. This makes it more difficult for anti-virus software or other security measures to detect and stop the malicious code from executing.

