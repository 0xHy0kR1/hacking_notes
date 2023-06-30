## Domain controller
- A domain controller is a server that manages and controls access to resources within a computer network.
- It is a central authority that governs user authentication, security policies, and the management of user accounts and permissions.
- Imagine a domain controller as the "gatekeeper" of a network.
- It holds the database of user accounts and passwords and verifies the identity of users when they try to log in to the network.
- By using a domain controller, organizations can establish a centralized system to manage and secure their network.

## Features
- It host a copy of the Active Directory domain service directory store.
- It provide authentication and authorization services.
- It replicate updates to other domain controllers in the domain and forest. 
- It allow administrative access to manage user accounts and network resources.

#### AD domain service directory store or Active Directory Domain Services database - 
- In simpler terms, the AD DS directory store is where all the data related to users, groups, computers, and other network resources is stored in a structured manner.
- It acts as a repository of information, allowing administrators to manage and organize these objects efficiently.
**Some imp points**
- It consists of the Ntds.dit file.
- It is stored by default in the %SystemRoot%\NTDS folder on all domain controllers.
- It is accessible only through the domain controller processes and protocols.
Everything like users data, group data and many more stored in the **Ntds.dit** file.