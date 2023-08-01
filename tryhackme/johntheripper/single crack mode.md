## Introduction
- In this mode, John uses only the information provided in the username, to try and work out possible passwords heuristically, by slightly changing the letters and numbers contained within the username.

### Word mangling 
- The best way to show what Single Crack mode is,  and what word mangling is, is to actually go through an example:
If we take the username: Markus

**Some possible passwords could be:**
- Markus1, Markus2, Markus3 (etc.)
- MArkus, MARkus, MARKus (etc.)
- Markus!, Markus$, Markus* (etc.)
This technique is called word mangling.
John is building it's own dictionary based on the information that it has been fed and uses a set of rules called "mangling rules"

#### GECOS
- John's implementation of word mangling also features compatibility with the Gecos fields of the UNIX operating system, and other UNIX-like operating systems such as Linux

##### What are the GECOS?
- In Unix-like operating systems, user account information is stored in a file called `/etc/passwd`.
- Each line in the `/etc/passwd` file represents a user account and contains several fields separated by colons (:).
- One of these fields is called the "GECOS" field, which stands for "General Electric Comprehensive Operating System." It is also known as the "comment field" because it initially stored comments about the user.
- The GECOS field contains information about the user, such as their full name, office location, and contact details. These pieces of information are separated by commas.
- Modern systems typically do not store actual password hashes in the `/etc/passwd` file for security reasons. Instead, they are stored in the `/etc/shadow` file, which is only accessible by the root user.

**Here's an example of a line in the `/etc/passwd` file:**
```bash
john:x:1000:1000:John Doe:/home/john:/bin/bash
```
In this example:

- Username: john
- Password field: 'x' (The actual password hash is stored in the `/etc/shadow` file on modern systems)
- User ID (UID): 1000
- Group ID (GID): 1000
- GECOS/Comment field: John Doe (This is the user's full name)

The GECOS field is not used for authentication purposes; it simply contains additional information about the user.

#### Using Single Crack Mode
**Example** - 
If we wanted to crack the password of the user named "Mike", using single mode, we'd use:
```python
john --single --format=[format] [path to file]
```
`--single` - This flag lets john know you want to use the single hash cracking mode.

**Example** - 
```python
john --single --format=raw-sha256 hashes.txt
```

**A Note on File Formats in Single Crack Mode:**
You need to change the file format by prepending the hash with the username that the hash belongs to, so according to the above example- we would change the file hashes.txt

**From:**  
1efee03cdcb96d90ad48ccc7b8666033
**To**
mike:1efee03cdcb96d90ad48ccc7b8666033

