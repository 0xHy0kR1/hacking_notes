You have been given the following organisational chart and are expected to make changes to the AD to match it:
![[AD_basics6.png]]

## Deleting extra OUs and users
- The first thing you should notice is that there is an additional department OU in your current AD configuration that doesn't appear in the chart.
- If you try to additional department OU then you will get the following error:
![[AD_basics7.png]]

**By default, OUs are protected against accidental deletion. To delete the OU, we need to enable the *Advanced Features* in the View menu:**
![[AD_basics8.png]]

**This will show you some additional containers and enable you to disable the accidental deletion protection. To do so, right-click the OU and go to Properties. You will find a checkbox in the Object tab to disable the protection:**
![[AD_basics9.png]]
- Be sure to uncheck the box and try deleting the OU again.
- You will be prompted to confirm that you want to delete the OU, and as a result, any users, groups or OUs under it will also be deleted.

## Delegation
- You can give specific users some control over some OUs. This process is known as **delegation** and allows you to grant users specific privileges to perform advanced tasks on OUs without needing a Domain Administrator to step in.

**Example** - 
One of the most common use cases for this is granting `IT support` the privileges to reset other low-privilege users' passwords.

##### For this example, we will delegate control over the Sales OU to Phillip(*Phillip is in charge of IT support*). To delegate control over an OU, you can right-click it and select Delegate Control:
![[AD_basics10.png]]

##### This should open a new window where you will first be asked for the users to whom you want to delegate control:
**Note:** - To avoid mistyping the user's name, write "phillip" and click the **Check Names** button. Windows will autocomplete the user for you.
![[AD_basics11.png]]

##### Click OK, and on the next step, select the following option:
![[AD_basics12.png]]
Click next a couple of times, and now Phillip should be able to reset passwords for any user in the sales department.

## Login via RDP
**Username** - phillip
**Password** - Claire2008
**Command** - 
```python
xfreerdp /v:<Windows_IP_Address> /u:<Username> /p:<Password>
```
**Note:** When connecting via RDP, use `THM\phillip` as the username to specify you want to log in using the user `phillip` on the `THM` domain.

**Password reset of "management" and "marketing" departments using powershell** - 
```powershell
PS C:\Users\phillip> Set-ADAccountPassword sophie -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password') -Verbose

New Password: *********

VERBOSE: Performing the operation "Set-ADAccountPassword" on target "CN=Sophie,OU=Sales,OU=THM,DC=thm,DC=local".
```

**Since we wouldn't want Sophie to keep on using a password we know, we can also force a password reset at the next logon with the following command:**
```powershell
PS C:\Users\phillip> Set-ADUser -ChangePasswordAtLogon $true -Identity sophie -Verbose

VERBOSE: Performing the operation "Set" on target "CN=Sophie,OU=Sales,OU=THM,DC=thm,DC=local".
```

