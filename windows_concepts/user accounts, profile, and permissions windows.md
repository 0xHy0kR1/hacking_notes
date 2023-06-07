User accounts are of two types in windows system: **Administrator** & **Standard User**.
The user account type will determine what actions the user can perform on that specific Windows system.

**Administrator**
- It can make changes to the system: add users, delete users, modify groups, modify settings on the system, etc.

**Standard User**
- It can only make changes to folders/files attributed to the user & can't perform system-level changes, such as install programs.

There are several ways to determine which user accounts exist on the system.
1. click the `Start Menu` and type `Other User`. A shortcut to `System Settings > Other users` should appear.
![[other_users_windows_stuff.png]]
Since you're the Administrator, you see an option to **Add someone else to this PC**.
**Note** - A Standard User will not see this option.

## Some points about user profile
- When a user account is created, a profile is created for the user.
- The location for each user profile folder will fall under is C:\Users.
For example, the user profile folder for the user account Max will be C:\Users\Max.

**Each user profile will have the same folders; a few of them are:**
- Desktop
- Documents
- Downloads
- Music
- Pictures

## Local User and Group Management
Right-click on the Start Menu and click **Run**. Type `lusrmgr.msc`.
![[user_and_group_management_windows_stuffs.png]]

If you click on Groups, you see all the names of the local groups along with a brief description for each group.
![[local_groups_windows_stuffs.png]]
When a user is assigned to a group, the user inherits the permissions of that group. A user can be assigned to multiple groups.

**Note** - If you click on **Add someone else to this PC** from **Other users**, it will open **Local Users and Management**.