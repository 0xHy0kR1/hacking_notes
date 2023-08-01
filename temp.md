In simple words, the attacker wants to place themselves between the target machine (Windows 10) and the internet, so they can control and manipulate the traffic passing between them.
- **ARP Spoofing attack** - In this case, the attacker uses the MITM framework to perform an ARP spoofing attack. It means that, ARP (Address Resolution Protocol) is used to map IP addresses to MAC addresses on a local network. ARP spoofing is a technique where the attacker sends fake ARP messages to the target and the router, tricking them into associating the attacker's MAC address with the IP address of the router (default gateway). As a result, the target machine sends its network traffic to the attacker instead of the actual router.

- **SSLstrip** - 
	- It is a tool that helps in bypassing the security provided by HTTPS connections.
	- Normally, when you visit a website with "https://" in the URL, it means the connection is secure. However, SSLstrip allows the attacker to convert these secure connections (HTTPS) into insecure connections (HTTP) without the user's knowledge.
	- It works by intercepting HTTPS requests from the target machine and converting them into HTTP requests, preventing secure encrypted communication. This way, the attacker can see the data being transmitted in plaintext, which makes it easier to manipulate or exploit.

- **Mapping HTTPS links to HTTP links:**
	- After SSLstrip has been deployed, any attempt by the target machine to visit an HTTPS website will be converted into an HTTP request. The attacker can then intercept the HTTP traffic and view its contents in plaintext.

- **Backdooring executables sent over HTTP:**
	- The Backdoor Factory is a tool used for injecting malicious code (backdoors) into legitimate software binaries.
	- In this context, the attacker leverages the fact that the target machine is now making HTTP requests instead of secure HTTPS requests. When the target machine attempts to download an executable (e.g., a software update or installation package) over HTTP, the attacker can use the Backdoor Factory to modify the executable, adding a backdoor to it. Once the target machine runs the modified executable, the backdoor will be installed, giving the attacker unauthorized access to the system.
- 