Go to **~/Documents/PowerView** to access powerview cheatsheet.

## Below small overview to PowerView:
**Before doing all the below stuffs make to install "PowerView" on the machine that where you are running below commands**

1. powershell -ep bypass --> It will help us on running powerview
2. . .\PowerView.ps1 --> running the "powerview" file
3. Get-NetDomain --> Taking out information about the domain
4. Get-NetDomainController --> Same command as previous one but it give us more infomation then that.
5. Get-DomainPolicy --> Listing domain policies
6. (Get-DomainPolicy)."system access" --> Listing system policy information 
7. Get-NetUser
8. Get-NetUser | select cn (OR) Get-NetUser | select samaccountname--> pull out all the usernames 
9. Get-NetUser | select description --> Listing the description of the user accounts
10. Get-UserProperty --> It show you all the properties that the user might have.
11. Get-UserProperty -Properties pwdlastset --> List users with when their password last set
12. Get-UserProperty -Properties logoncount --> the user that doesn't login before, might be a honeypot account
13. Get-UserProperty -Properties badpwdcount --> List the all accounts on the basis of bad password
14. Get-NetComputer
15. Get-NetComputer -FullData
16. Get-NetComputer -FullData | select OperatingSystem
17. Get-NetGroup
18. Get-NetGroup -GroupName "Domain Admins"
19. Get-NetGroup -GroupName *admin*
20. Get-NetGroupMember -GroupName "Domain Admins"
21. Invoke-ShareFinder
22. Get-NetGPO
23. Get-NetGPO | select displayname, whenchanged
