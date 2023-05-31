- Register in their offical website with this link
www.tenable.com/products/nessus/nessus-essentials
after that they sent activation code through email and download nessus from email

- After above step for kali linux install the .deb file which you downloaded and after that do the following steps as described in below image to open nessus via browser
![[nessus_steps.png]]
- To start working with Nessus in msfconsole, we will have to load Nessus and then connect it with the server to start our penetration testing

- First, we will launch msfconsole and load the nessus plugin
	 ```python
	 msf6 > load nessus
	[*] Nessus Bridge for Metasploit
	[*] Type nessus_help for a command listing
	[*] Successfully loaded plugin: Nessus
```

- By running the nessus_help command, we can display all the available commands:
	 ```python
	 msf6 > nessus_help

	Command                     Help Text
	-------                     ---------
	Generic Commands
	-----------------           -----------------
	nessus_connect              Connect to a Nessus server```

 - To connect to Nessus, use the nessus_connect command with the Nessus credentials, hostname, port (if not using the default port 8834), and verify the SSL certificate.
	```python
	msf6 > nessus_connect helloweenhell666@gmail.com:"xcthello@me here"@127.0.0.1
	[*] Connecting to https://127.0.0.1:8834/ as helloweenhell666@gmail.com
	[*] User helloweenhell666@gmail.com authenticated successfully.```

- Using the nessus_policy_list command, we can list all policies on the server; before using Nessus via msfconsole, you need to connect to the Nessus GUI and create a policy before being able to use it:
```python
	msf6 > nessus_policy_list
	[-] No policies found```

- 