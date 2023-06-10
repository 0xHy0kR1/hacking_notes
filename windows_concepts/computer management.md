The **Computer Management** (`compmgmt`) utility has three primary sections: System Tools, Storage, and Services and Applications.
![[computer_management1_windows_stuffs.png]]

### System Tools
1. Task Scheduler
	we can create and manage common tasks that our computer will carry out automatically at the times we specify.

	To create a basic task, click on `Create Basic Task` under **Actions** (right pane).
	![[computer_management2_windows_stuff.png]]

2. Event Viewer
	Event Viewer allows us to view events that have occurred on the computer. It can be used to understand the activity of the computer system.
![[computer_management3_windows_stuff.png]]

**The following table describes the five event types used in event logging**
1. **Error**
	- An event that indicates a significant problem such as loss of data or loss of functionality.
	- For example, if a service fails to load during startup, an Error event is logged.

2. **Warning**
	- An event that is not necessarily significant, but may indicate a possible future problem.
	- For example, when disk space is low, a Warning event is logged.

3. **Information**
	- An event that describes the successful operation of an application, driver, or service.
	- For example, when a network driver loads successfully, it may be appropriate to log an Information event.

4. **Success Audit**
	- generate an audit entry when a logon attempt succeeds.
	- For example, a user's successful attempt to log on to the system is logged as a Success Audit event.

5. **Failure Audit**
	- This event is generated when an account logon attempt failed, assuming the user was already locked out.
	- For example, if a user tries to access a network drive and fails, the attempt is logged as a Failure Audit event.

## Standard logs
The standard logs are visible under Windows Logs.

1. **Application**
	- Contains events logged by applications.
	- For example, a database application might record a file error.

2. **Security**
	- Contains events such as valid and invalid logon attempts, as well as events related to resource use such as creating, opening, or deleting files or other objects.

3. System
	- Contains events logged by system components, such as the failure of a driver.

## Shared folders

### Shares
- **Shared Folders** is where you will see a complete list of shares and folders shared that others can connect to.
![[shared_folders1_windows_stuffs.png]]
- In the above image, under Shares, are the default share of Windows, C$.
- default remote administration shares created by Windows, such as ADMIN$.

### Sessions
- Under **Sessions**, you will see a list of users who are currently connected to the shares
![[computer_management4_windows_stuff.png]]

### Open Files
- All the folders and/or files that the connected users access will list under **Open Files**.
![[computer_management5_windows_stuffs.png]]

## Local Users and Groups
Related --> [[user accounts, profile, and permissions windows]]

## Performance
- In **Performance**, you'll see a utility called **Performance Monitor** (`perfmon`).
![[computer_management6_windows_stuffs.png]]
- Perfmon is used to view performance data either in real-time or from a log file.
- This utility is useful for troubleshooting performance issues on a computer system, whether local or remote.

## Device Manager
It allows us to view and configure the hardware, such as disabling any hardware attached to the computer.
![[computer_management7_windows_stuffs.png]]

## Storage
Under Storage is **Windows Server Backup** and **Disk Management**.
![[computer_management8_windows_stuffs.png]]

### Disk Management
Disk Management is a system utility in Windows that enables you to perform advanced storage tasks.

Some tasks are:
- Set up a new drive
- Extend a partition
- Shrink a partition
- Assign or change a drive letter (ex. E:)
![[computer_management9_windows_stuffs.png]]

## Services and Applications
- a service is a special type of application that runs in the background.
- Here you can do more than enable and disable a service, such as view the Properties for the service.

### WMI control
WMI allows scripting languages (such as VBScript or Windows PowerShell) to manage Microsoft Windows personal computers and servers, both locally and remotely.
![[computer_management10_windows_stuffs.png]]
Microsoft also provides a command-line interface to WMI called Windows Management Instrumentation Command-line (WMIC).

**Note**: The WMIC tool is deprecated in Windows 10, version 21H1. Windows PowerShell supersedes this tool for WMI.