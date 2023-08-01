## Cracking SSH Key Passwords
- Using John to crack the SSH private key password of id_rsa files.
- Unless configured otherwise, you authenticate your SSH login using a password. However, you can configure key-based authentication, which lets you use your private key, id_rsa, as an authentication key to login to a remote machine over SSH.
- However, doing so will often require a password- here we will be using John to crack this password to allow authentication over SSH using the key.

## SSH2John
- id_rsa private key that you use to login to the SSH session into hash format that john can work with.
**Syntax** - 
```python
ssh2john [id_rsa private key file] > [output file]
```
`[id_rsa private key file]` - The path to the id_rsa file you wish to get the hash of

`>` - This is the output director, we're using this to send the output from this file to the...  

`[output file]` - This is the file that will store the output from

**Example** - 
```python
ssh2john id_rsa > id_rsa_hash.txt
```

## Cracking
```python
john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt
```

