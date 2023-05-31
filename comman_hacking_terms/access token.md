- In Windows, an access token is a data structure.
- It contains information about a user or a process, including their security identifiers(SIDs), privileges, and group memberships.
- When a user logs in to a Windows system, the operating system creates an access token that identifies the user and their security context.
- Similarly, when a process is launched, the operating system creates a access token that identifies the process and its associated surity context.
- For example, when a user or a process tries to access a resource, the operating system checks their access token to determine whether they have the required permissions and privileges.
## There are two types of tokens: 
1. Delegate tokens - 
- Delegate tokens are used for interactive logins, where the user needs to interact with the system directly.

2. Impersonate tokens -
- tokens are used for noninteractive sessions, where the user's actions are automated and don't require direct interaction with the system.