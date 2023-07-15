## Introduction
- A very common and easy attack that provides user credentials stored in SYSVOL share that can be used to get a shell or escalate privileges.
- Group Policy Preferences (GPP) allowed administrators to create domain policies with embedded credentials.
- Group Policy Preferences allow administrators to manage and configure various settings on multiple computers within a domain.
- In simple terms, GPP is a tool that provides some advanced capabilities to administrators for configuring and managing account policy in a Windows domain network.
- When a new Group Policy Preference (GPP) is generated, a xml file (generally Groups.xml) with the configuration data, including any passwords associated with the GPP, is created in the SYSVOL share which are folders on domain controllers accessible and readable to all authenticated domain users.
- The key was accidentally released. This issue patched in MS14-025, but doesn't prevent previous uses.

**The Domain Group Policies are stored at:**
```python
\\<DOMAIN>\SYSVOL\<DOMAIN>\Policies\
```

**The cpassword stored in XML file looks like:**
![[AD_post25.png]]

**So there are some scenarios in which we can read these files:**
- We already have a low privileged shell on the system so we can search for the XML file in SYSVOL share.
- We are able to access SMB file shares anonymously (without any passwords) due to guest access allowed and that share has XML file hosted.
- Any Other Vulnerablity that exposes or allow access to XML file.

## Practical implementation
In this implementation, we perform all of this on HTP Active machine.

1. nmap scan
![[gpp1.png]]

nmap output after the scan so far.
![[gpp2.png]]

2. connecting to smb share because as previously discussed may be that gpp file hosted in the share 
**list out the shares**
![[gpp3.png]]

**connecting to "Replication" share may be we can get access.**
![[gpp4.png]]

3. finally got that file in the share.
![[gpp5.png]]

![[gpp6.png]]

4. Looking inside of that file and we get the **cpassword**.
![[gpp7.png]]

5. Now, we decrypt the hash to access spn.
![[gpp8.png]]

6. Start the attack and we get the kerberos hash.
![[gpp9.png]]

7. Now, we try to gain a administrative shell on that machine and we success it.
![[gpp10.png]]
