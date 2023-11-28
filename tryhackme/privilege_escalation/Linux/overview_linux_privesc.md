## What does "privilege escalation" mean?
- At it's core, Privilege Escalation usually involves going from a lower permission to a higher permission.
- More technically, it's the exploitation of a vulnerability, design flaw or configuration oversight in an operating system or application to gain unauthorized access to resources that are usually restricted from the users.

## Why is it important?
Privilege escalation is crucial, because it lets you gain system administrator levels of access.

**This allow you to do many things, including:**
-  Reset passwords  
-  Bypass access controls to compromise protected data
-  Edit software configurations
-  Enable persistence, so you can access the machine again later.
-  Change privilege of users
-  Get that cheeky root flag ;)

## Direction of privilege escalation - 
![[linux_privesc1.png]]


#### There are two main privilege escalation variants:
###### Horizontal privilege escalation:
- This is where you expand your reach over the compromised system by taking over a different user who is on the same privilege level as you.
- This allows you to inherit whatever files and access that user has.
- This can be used, for example, to gain access to another normal privilege user, that happens to have an SUID file attached to their home directory, which can then be used to get super user access.

###### Vertical privilege escalation:
This is where you attempt to gain higher privileges or access, with an existing account that you have already compromised.

