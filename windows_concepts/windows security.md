## Status icons
- **Green** means your device is sufficiently protected, and there aren't any recommended actions.
- **Yellow** means there is a safety recommendation for you to review.
- **Red** is a warning that something needs your immediate attention.
![[windows_security1_windows_stuffs.png]]

## Virus & threat protection
![[virus_threat1_windows_stuffs.png]]

### Current threats

#### Scan options
![[virus_threat2_windows_stuffs.png]]

#### Threat history
![[virus_threat3_windows_stuffs.png]]

## Firewall & network protection
![[firewall_network_protection1_windows_stuffs.png]]

**The Windows Firewall has three profiles, domain, private and public.**

**Domain profile:** This profile applies to networks where the computer can authenticate to a domain controller.

**Private profile:** This profile is a user assigned profile and is used for private and home networks.

**Public profile:** This is used when connected to public networks such as public wifi.

### allow an app through firewall
![[firewall_network_protection2_windows_stuffs.png.png]]
**Configuring the Windows Defender Firewall for advanced Windows users. Take a look [here](https://docs.microsoft.com/en-us/windows/security/threat-protection/windows-firewall/best-practices-configuring)

**Note** - Command to open the Windows Defender Firewall is `WF.msc`.

## Apps and browser control
![[app_browser_control1_windows_stuffs.png]]

### Microsoft defender smart screen control
**Windows Defender SmartScreen** helps protect your device by checking for unrecognized apps and files from the web.
![[app_browser_control2_windows_stuffs.png]]

## Device security
![[device_security1_windows_stuffs.png]]

### Security processor
![[device_security2_windows_stuffs.png]]
Trusted Platform Module (TPM) is a hardware component that provides security-related functions for computers and other devices.
Think of it as a small, specialized chip that helps protect your data and ensure the integrity of your system.
TPM acts like a security guard for your computer, keeping an eye on things and making sure everything is in order. It has its own memory and processing power, separate from the main processor of your device. Its main purpose is to securely store and manage encryption keys, which are used to protect sensitive information.

## BitLocker
- BitLocker is a disk encryption feature provided by Microsoft that helps protect the data on your computer's storage drive.
- It is available in certain versions of Windows, such as Windows 10 Pro, Enterprise, and Education.
- When you enable BitLocker on a drive, it encrypts the contents of that drive, making the data unreadable without the correct encryption key.

**What must a user insert on computers that **DO NOT** have a TPM version 1.2 or later?**
Ans - **Usb startup key**
