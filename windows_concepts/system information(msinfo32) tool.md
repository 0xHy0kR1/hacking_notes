## Introduction
- Windows includes a tool called Microsoft System Information (Msinfo32.exe).
- This tool gathers information about your computer and displays a comprehensive view of your hardware, system components, and software environment, which you can use to diagnose computer issues.
![[system_info1_windows_stuffs.png]]

**The  information in System Summary is divided into three sections:**
- Hardware Resources
- Components
- Software Environment
![[system_info2_windows_stuffs.png]]

### Hardware Resources
The information displayed in **Hardware Resources** is not for the average computer user.

### Components
Under **Components**, you can see specific information about the hardware devices installed on the computer
![[system_info3_windows_stuffs.png]]

### Software Environment
In the **Software Environmen**t section, you can see information about software baked into the operating system and software you have installed.
Other details are visible in this section as well, such as the **Environment Variables** and **Network Connections**.
![[system_info4_windows_stuffs.png]]

**Environment variables**
- Environment variables store information about the operating system environment.
- This information includes details such as the operating system path, the number of processors used by the operating system, and the location of temporary folders.
For example, the WINDIR environment variable contains the location of the Windows installation directory. Programs can query the value of this variable to determine where Windows operating system files are located

**Click on `Environment Variables` to see the assigned values for the virtual machine**
![[system_info5_windows_stuffs.png]]

**Another method to view environment variables is**
`Control Panel > System and Security > System > Advanced system settings > Environment Variables` **OR** `Settings > System > About > system info > Advanced system settings > Environment Variables`.