Monitor `HKLM\Software\Policies\Microsoft\Windows NT\DNSClient` for changes to the "EnableMulticast" DWORD value. A value of "0" indicates LLMNR is disabled.

Monitor for traffic on ports UDP 5355 and UDP 137 if LLMNR/NetBIOS is disabled by security policy.

Deploy an LLMNR/NBT-NS spoofing detection tool. Monitoring of Windows event logs for event IDs 4697 and 7045 may help in detecting successful relay techniques.​