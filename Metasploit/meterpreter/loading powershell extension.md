## loading the PowerShell extension
```python
meterpreter > load powershell
Loading extension powershell...Success.
```

## Powershell execute command
```python
meterpreter > powershell_execute $PSVersionTable
[+] Command execution completed:

Name                           Value
----                           -----
PSVersion                      5.1.14409.1005
PSEdition                      Desktop
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
BuildVersion                   10.0.14409.1005
CLRVersion                     4.0.30319.34209
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
SerializationVersion           1.1.0.1
```
- This command retrieves the information about the version and configuration of the PowerShell environment that is currently running like its version number(5.1.14409.1005), edition of PowerShell(Desktop), compatible versions of PowerShell, etc.

## Using multiple powershell commands
```python
meterpreter > powershell_execute "Get-WmiObject Win32_UserDesktop | Select-Object Element"
[+] Command execution completed:

Element
-------
\\VAGRANT-2008R2\root\cimv2:Win32_UserAccount.Domain="VAGRANT-2008R2",Name="Administrator"
\\VAGRANT-2008R2\root\cimv2:Win32_UserAccount.Domain="VAGRANT-2008R2",Name="anakin_skywalker"
\\VAGRANT-2008R2\root\cimv2:Win32_UserAccount.Domain="VAGRANT-2008R2",Name="artoo_detoo"
\\VAGRANT-2008R2\root\cimv2:Win32_UserAccount.Domain="VAGRANT-2008R2",Name="ben_kenobi"
\\VAGRANT-2008R2\root\cimv2:Win32_UserAccount.Domain="VAGRANT-2008R2",Name="boba_fett"
\\VAGRANT-2008R2\root\cimv2:Win32_UserAccount.Domain="VAGRANT-2008R2",Name="chewbacca"
\\VAGRANT-2008R2\root\cimv2:Win32_UserAccount.Domain="VAGRANT-2008R2",Name="c_three_pio"
\\VAGRANT-2008R2\root\cimv2:Win32_UserAccount.Domain="VAGRANT-2008R2",Name="darth_vader"
\\VAGRANT-2008R2\root\cimv2:Win32_UserAccount.Domain="VAGRANT-2008R2",Name="greedo"
\\VAGRANT-2008R2\root\cimv2:Win32_UserAccount.Domain="VAGRANT-2008R2",Name="Guest"
\\VAGRANT-2008R2\root\cimv2:Win32_UserAccount.Domain="VAGRANT-2008R2",Name="han_solo"
\\VAGRANT-2008R2\root\cimv2:Win32_UserAccount.Domain="VAGRANT-2008R2",Name="jabba_hutt"
\\VAGRANT-2008R2\root\cimv2:Win32_UserAccount.Domain="VAGRANT-2008R2",Name="jarjar_binks"
\\VAGRANT-2008R2\root\cimv2:Win32_UserAccount.Domain="VAGRANT-2008R2",Name="kylo_ren"
\\VAGRANT-2008R2\root\cimv2:Win32_UserAccount.Domain="VAGRANT-2008R2",Name="lando_calrissian"
\\VAGRANT-2008R2\root\cimv2:Win32_UserAccount.Domain="VAGRANT-2008R2",Name="leia_organa"
\\VAGRANT-2008R2\root\cimv2:Win32_UserAccount.Domain="VAGRANT-2008R2",Name="luke_skywalker"
\\VAGRANT-2008R2\root\cimv2:Win32_UserAccount.Domain="VAGRANT-2008R2",Name="sshd"
\\VAGRANT-2008R2\root\cimv2:Win32_UserAccount.Domain="VAGRANT-2008R2",Name="sshd_server"
\\VAGRANT-2008R2\root\cimv2:Win32_UserAccount.Domain="VAGRANT-2008R2",Name="vagrant"
```
- This command retrieves the information about the currently logged-on user's desktop environment.
- Let's break down the command
	- "Get-WmiObject" is a PowerShell  cmdlet that retrieves information from windows management instrumentation(WMI) classes.
	- "Win32_UserDesktop" is the specific WMI class that is being queried. This class contains information about the desktop environment of the current user. 
	- "Select-Object Element" is another PowerShell cmdlet that selects a specific property from the output of the previous command. In this case, it selects the "Element" property of the "Win32_UserDesktop" WMI class.