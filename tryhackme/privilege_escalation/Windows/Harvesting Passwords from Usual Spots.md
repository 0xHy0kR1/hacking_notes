## Unattended Windows Installations

   - When installing Windows on a large number of hosts, administrators may use Windows Deployment Services, which allows for a single operating system image to be deployed to several hosts through the network.
   - These kinds of installations are referred to as unattended installations as they don't require user interaction.

**Such installations require the use of an administrator account to perform the initial setup, which might end up being stored in the machine in the following locations:**
   - C:\Unattend.xml
   - C:\Windows\Panther\Unattend.xml
   - C:\Windows\Panther\Unattend\Unattend.xml
   - C:\Windows\system32\sysprep.inf
   - C:\Windows\system32\sysprep\sysprep.xml

**As part of these files, you might encounter credentials:**
```xml
<Credentials>
    <Username>Administrator</Username>
    <Domain>thm.local</Domain>
    <Password>MyPassword123</Password>
</Credentials>
```

## Powershell History

   - Whenever a user runs a command using Powershell, it gets stored into a file that keeps a memory of past commands. This is useful for repeating commands you have used before quickly.
   - If a user runs a command that includes a password directly as part of the Powershell command line, it can later be retrieved by using the following command from a `cmd.exe` prompt:

```powershell
type %userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt
```

**Note:**
   The command above will only work from cmd.exe, as Powershell won't recognize `%userprofile%` as an environment variable. To read the file from Powershell, you'd have to replace `%userprofile%` with `$Env:userprofile`.

## Saved Windows Credentials

   - Windows allows us to use other user's credentials. This function also gives the option to save these credentials on the system.
   - The command below will list saved credentials:
```powershell
cmdkey /list
```

**If you notice any credentials worth trying, you can use them with the `runas` command and the `/savecred` option, as seen below.**
```powershell
runas /savecred /user:user_name cmd.exe
```
 
## IIS Configuration

   - Internet Information Services (IIS) is the default web server on Windows installations.
   - The configuration of websites on IIS is stored in a file called `web.config` and can store passwords for databases or configured authentication mechanisms.

**Depending on the installed version of IIS, we can find web.config in one of the following locations:**
   - `C:\inetpub\wwwroot\web.config`
   - `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config`

**Here is a quick way to find database connection strings on the file:**
```powershell
type C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config | findstr connectionString
```

## Retrieve Credentials from Software: PuTTY

   - PuTTY is an SSH client commonly found on Windows systems.
   - Instead of having to specify a connection's parameters every single time, users can store sessions where the IP, user and other configurations can be stored for later use. While PuTTY won't allow users to store their SSH password, it will store proxy configurations that include cleartext authentication credentials.
**To retrieve the stored proxy credentials, you can search under the following registry key for ProxyPassword with the following command:**
```powershell
reg query HKEY_CURRENT_USER\Software\SimonTatham\PuTTY\Sessions\ /f "Proxy" /s
```

#### Note
   - Simon Tatham is the creator of PuTTY (and his name is part of the path), not the username for which we are retrieving the password. The stored proxy username should also be visible after running the command above.
   - Just as putty stores credentials, any software that stores passwords, including browsers, email clients, FTP clients, SSH clients, VNC software and others, will have methods to recover any passwords the user has saved.

```sh
xfreerdp /v:10.10.48.108 /u:Administrator /p:letmein123!
```



