## Introduction
- By default, all the machines that join a domain (except for the DCs) will be put in the container called "Computers".
- If we check our DC, we will see that some devices are already there:
![[AD_basics13.png]]

## In general, you'd expect to see devices divided into at least the three following categories:

#### 1. Workstations
This is the device they will use to do their work or normal browsing activities. These devices should never have a privileged user signed into them.

#### 2. Servers
Servers are the second most common device within an Active Directory domain. Servers are generally used to provide services to users or other servers.

#### 3. Domain Controllers
- Domain Controllers are the third most common device within an Active Directory domain.
- Domain Controllers allow you to manage the Active Directory Domain.
- These devices are often deemed the most sensitive devices within the network as they contain hashed passwords for all user accounts within the environment.
- let's create two separate OUs for `Workstations` and `Servers`. We will be creating them directly under the `thm.local` domain container. 
![[AD_basics14.png]]
Now, move the personal computers and laptops to the Workstations OU and the servers to the Servers OU from the Computers container. Doing so will allow us to configure policies for each OU later.

