## Introduction to KRBTGT account in AD
- the most powerful service account in any Active Directory environment: the KRBTGT account, which is used to issue the Kerberos tickets required to access IT systems and data.
- By obtaining the password hash for this account from the Key Distribution Center (KDC), an attacker is able to compromise every account in Active Directory, giving them unlimited and virtually undetectable access to any system connected to the AD network.
- Windows Active Directory domain controllers are responsible for handling Kerberos ticket requests, which are used to authenticate users and grant them access to computers and applications.
- The KRBTGT account’s password is used to encrypt and decrypt Kerberos tickets.
- This password rarely changes and the account name is the same in every domain, so it is a common target for attackers.

## Creating Golden Tickets
Using [Mimikatz](https://github.com/gentilkiwi/mimikatz), it is possible to leverage the password of the KRBTGT account to create forged Kerberos Ticket Granting Tickets (TGTs) which can be used to request Ticket Granting Server (TGS) tickets for any service on any computer in the domain.

**To create Kerberos Golden Tickets, an adversary needs the following information:**
- KRBTGT account password hash
- The name and SID of the domain to which the KRBTGT account belongs

### Step 1. Obtain the KRBTGT password hash and domain name and SID.
- Obtaining the KRBTGT password hash is the hardest part of the attack because it requires gaining privileged access to a domain controller.
- Once an adversary is able to log on interactively or remotely to a DC, they can use Mimikatz to extract the required information using the following commands:
```python
privilege::debug
lsadump::lsa /inject /name:krbtgt
```

**This will output the password hash, as well as the domain name and SID:**
![[golden_ticket_attack.png]]

### Step 2. Create Golden Tickets.
**Useful Mimikatz parameters for creating Golden Tickets include:**

**User**— The name of the user account the ticket will be created Note that this can be a valid account name, but it doesn’t have to be.

**ID**— The RID of the account the attacker will be impersonating. This could be a real account ID, such as the default administrator ID of 500, or a fake ID.

**Groups**— A list of groups to which the account in the ticket will belong. Domain Admins is included by default so the ticket will be created with maximum privileges.

**SIDs**— This will insert a SID into the SIDHistory attribute of the account in the ticket. This is useful to authenticate across domains.

The following example creates a ticket for a fake user but provides the default administrator ID
The **/ptt** (Pass the Ticket) trigger injects the Golden Ticket being created into the current session.

**Command** - 
```python
 kerberos::golden /User:Administrator /domain:marvel.local /sid:S-1-5-21-301214212-3920777931-1277971883 /krbtgt:11f843aafd22acfb29aef92f6e423994 /id:500 /ptt
```

**Below output** - 
![[golden_ticket_attack2.png]]

### Step 3. Pass the ticket.
- Now it is time to use the Golden Ticket that was loaded into the current session.
- Let’s launch a command prompt under the context of that ticket using the **misc::cmd** command.

**Command** - 
```python
misc::cmd
```

**Below, you can see in the command prompt that the attacker operates as a regular domain user with no domain group membership, which means they should have no rights to any other domain computers.**
![[golden_ticket_attack3.png]]

**However, because the Kerberos ticket is in memory, it’s possible to connect to a domain controller and gain access to all of the files stored there.**
![[golden_ticket_attack4.png]]

**Note** - 
1. The system believes the attacker is the Administrator because of the RID of 500 they used to generate the Golden Ticket.
2. The event logs on the domain controller also show that system believes the attacker is the Administrator, but the credentials are the one that were spoofed during the Golden Ticket attack.

**Optional** --> If the below one doesn't work then move on.
Using [PSExec](https://docs.microsoft.com/en-us/sysinternals/downloads/psexec), the attacker can open a session on the target domain controller; according to that session, they are now logged in as Administrator.
**Command** - 

```python
C:\Users\Administrator\Downloads\paexec.exe \\Administrator cmd.exe
```

**Source** --> https://blog.netwrix.com/2022/08/31/complete-domain-compromise-with-golden-tickets/
