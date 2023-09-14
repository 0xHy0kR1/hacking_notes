## Introduction
- The core of any Windows Domain is the **Active Directory Domain Service (AD DS)**.
- This service acts as a catalogue that holds the information of all of the "objects" that exist on your network.
- Amongst the many objects supported by AD, we have users, groups, machines, printers, shares and many others.

#### Users
Users are one of the objects known as **security principals**, meaning that they can be authenticated by the domain and can be assigned privileges over **resources** like files or printers.

**Users can be used to represent two types of entities:**
- **People:** users will generally represent persons in your organisation that need to access the network, like employees.
- **Services:**
	- you can also define users to be used by services like IIS or MSSQL.
	- Every single service requires a user to run, but service users are different from regular users as they will only have the privileges needed to run their specific service.

#### Machines
- for every computer that joins the Active Directory domain, a machine object will be created.
- Machines are also considered "security principals" and are assigned an account just as any regular user. This account has somewhat limited rights within the domain itself.
- The machine accounts themselves are local administrators on the assigned computer, they are generally not supposed to be accessed by anyone except the computer itself, but as with any other account, if you have the password, you can use it to log in.
- The machine account name is the computer's name followed by a dollar sign.
**Example** - 
a machine named `DC01` will have a machine account called `DC01$`.

#### Security Groups
- In windows, you can define user groups to assign access rights to files or other resources to entire groups instead of single users. This allows for better manageability as you can add users to an existing group, and they will automatically inherit all of the group's privileges.
- Security groups are also considered security principals and, therefore, can have privileges over resources on the network.
- Groups can have both users and machines as members. If needed, groups can include other groups as well.
- Several groups are created by default in a domain that can be used to grant specific privileges to users.
**Example** - here are some of the most important groups in a domain:
![[AD_basics2.png]]

## Active Directory Users and Computers
To configure users, groups or machines in Active Directory, we need to log in to the Domain Controller and run "Active Directory Users and Computers" from the start menu:
![[AD_basics3.png]]

### Organizational Units(OUs)
- These objects are organised in **Organizational Units (OUs)** which are container objects that allow you to classify users and machines.
- OUs are mainly used to define sets of users with similar policing requirements. The people in the Sales department of your organisation are likely to have a different set of policies applied than the people in IT, for example. Keep in mind that a user can only be a part of a single OU at a time.
- Checking our machine, we can see that there is already an OU called `THM` with four child OUs for the IT, Management, Marketing and Sales departments.
![[AD_basics4.png]]
- Feel free to right-click the `THM` OU and create a new OU under it called `Students`
- If you open any OUs, you can see the users they contain.
![[AD_basics5.png]]

### Other containers(except THM)
- **Builtin:** Contains default groups available to any Windows host.
- **Computers:** Any machine joining the network will be put here by default. You can move them if needed.
- **Domain Controllers:** Default OU that contains the DCs in your network.
- **Users:** Default users and groups that apply to a domain-wide context.
- **Managed Service Accounts:** Holds accounts used by services in your Windows domain.

### Security Groups vs OUs
**OUs**
- **OUs** are handy for **applying policies** to users and computers, which include specific configurations depending on their particular role in the enterprise.
- Remember, a user can only be a member of a single OU at a time.

**Security Groups**
- **Security Groups**, on the other hand, are used to **grant permissions over resources**.
**Example** - 
you will use groups if you want to allow some users to access a shared folder or network printer.
A user can be a part of many groups, which is needed to grant access to multiple resources.