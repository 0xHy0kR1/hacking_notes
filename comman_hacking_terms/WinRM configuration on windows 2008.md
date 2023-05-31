- Run the following command to enable WinRM:
 ```bash
 winrm quickconfig
```

This command will configure WinRM to allow remote access and enable the firewall exception for WinRM.

- If you want to enable HTTPS for secure remote access, you'll need to configure a certificate. To do this, run the following command:
```lua
winrm create winrm/config/Listener?Address=*+Transport=HTTPS @{Hostname="<hostname>";CertificateThumbprint="<thumbprint>"}
```
Replace `<hostname>` with the fully-qualified domain name of the computer, and `<thumbprint>` with the thumbprint of the SSL certificate that you want to use.

- To verify that WinRM is configured correctly, run the following command to display the current WinRM configuration:
```python
winrm get winrm/config
```
This command will display the current configuration of WinRM, including the listening addresses and ports.