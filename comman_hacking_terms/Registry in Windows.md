The Windows Registry is a hierarchical database that stores configuration settings and options for the operating system, installed applications, and user preferences.

## Structure
The registry is organized into a tree-like structure, with the root of the tree represented by five keys, each of which contains multiple subkeys:

#### HKEY_CLASSES_ROOT
- When you double-click on a file on your computer, Windows uses this branch of the registry to determine which program should be used to open the file.
- It also contains information about OLE(Object Linking and Embedding) object classes, which are used by some programs to share data between applications.

#### HKEY_CURRENT_USER
- This branch of the registry contains settings specific to the currently logged-in user.
- When you log in to your Windows account, the system uses this branch of the registry to store settings like your desktop wallpaper, Start menu layout, and other preferences.
- Each user account on the computer has its own `HKEY_CURRENT_USER`.

#### HKEY_LOCAL_MACHINE
- This branch of the registry contains settings that apply to the entire system, as well as settings specific to individual hardware components and installed applications.
- This is where you'll find settings like system-wide font settings, network settings, and device driver information.
- It also has subkeys that are specific to certain hardware components and software applications.

#### HKEY_USERS
- This branch of the registry contains subkeys for all user accounts on the system, including the default user profile and any currently logged-in users.
- Each user account on the computer has its own subkey, which stores the settings specific to that user.
- This branch is similar to the `HKEY_CURRENT_USER` branch, but it includes settings for all users, not just the currently logged-in user.

#### HKEY_CURRENT_CONFIG
- This branch of the registry contains information about the current hardware profile.
- When you start up your computer, Windows detects your hardware and creates a hardware profile. This branch of the registry stores information about that hardware profile, including settings related to hardware components like your monitor and sound card.

## Values in key and subkey
- In the Windows Registry, each key and subkey can contain values, which are used to store different types of configuration settings, preferences, and other information. Below there are some common values

#### String
- A string value is used to store text data, such as a name or a path.
- For example, a key might hava a string value called "Name" with a value of "John Doe".

#### Binary
- A binary value is used to store binary data, such as executable files or images files.
- A binary value called "Icon" that stores the icon file in binary format.

#### DWORD 
- A DWORD value is used to store 32-bit integer data, such as a number or a flag.
- For example, a key might have a DWORD value called "Enabled" with a value of "1" to indicate that a feature is enabled.

#### QWORD
- A QWORD value is used to store 64-bit integer data, such as a large number or a timestamp. 
- For example, a key might have a QWORD value called "Timestamp" with a value of "1523456789" to indicate specific date and time.

#### Expandable String
- An expandable string value is used to store text data that can be expanded at runtime, such as environment variables or file paths.
- For example, a key might have an expandable string value called "Path" with a value of "%SystemRoot%\\system32" which can be expanded to "C:\\Windows\\system32" at runtime.

## Registry Editing Tools
- Regedit
- Regedt32
- PowerShell