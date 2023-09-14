### Unix password hashes
- Unix style password hashes are very easy to recognise, as they have a prefix.
- The prefix tells you the hashing algorithm used to generate the hash. The standard format is`$format$rounds$salt$hash`.

**Here's a quick table of the most Unix style password prefixes** - 
![[hash1.png]]

**Note** - On Linux, password hashes are stored in /etc/shadow. This file is normally only readable by root.
### Windows password hashes
- Windows passwords are hashed using NTLM, which is a variant of md4.
- They're visually identical to md4 and md5 hashes.
- On Windows, password hashes are stored in the SAM.
- Windows tries to prevent normal users from dumping them, but tools like mimikatz exist for this. Importantly, the hashes found there are split into NT hashes and LM hashes.

