privilege escalation consists of using given access to a host with "user A" and leveraging it to gain access to "user B" by abusing a weakness in the target system.

**Depending on the situation, we might need to abuse some of the following weaknesses:**
   - Misconfigurations on Windows services or scheduled tasks
   - Excessive privileges assigned to our account
   - Vulnerable software
   - Missing Windows security patches

## Windows Users

   Windows systems mainly have two kinds of users. Depending on their access levels, we can categorise a user in one of the following groups:
   ![[windows_privesc1.png]]
   - Any user with administrative privileges will be part of the **Administrators** group.
   - On the other hand, standard users are part of the **Users** group.

**In addition to that, you will usually hear about some special built-in accounts used by the operating system in the context of privilege escalation:**
![[windows_privesc2.png]]
- These accounts are created and managed by Windows, and you won't be able to use them as other regular accounts.
- Still, in some situations, you may gain their privileges due to exploiting specific services.

