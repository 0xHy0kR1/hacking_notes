### Automatic Cracking
John has built-in features to detect what type of hash it's being given, and to select appropriate rules and formats to crack it for you, this isn't always the best idea as it can be unreliable- but if you can't identify what hash type you're working with and just want to try cracking it, it can be a good option!

**Syntax** - 
```python
john --wordlist=[path to wordlist] [path to file]
```
`--wordlist=` - Specifies using wordlist mode, reading from the file that you supply in the following path...
`[path to wordlist]` - The path to the wordlist you're using, as described in the previous task.

**Example** - 
```python
john --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt
```

### Identifying Hashes
For identifying hashes you can use online [websites](https://hashes.com/en/tools/hash_identifier) or tool called hash-identifier.
```python
┌──(hoax㉿kali)-[~/thm/first_task_hashes]
└─$ hash-identifier 
```
and give hash value, when it ask for that.

### Format-Specific Cracking
**Syntax** - 
```python
john --format=[format] --wordlist=[path to wordlist] [path to file]
```
`--format=` - This is the flag to tell John that you're giving it a hash of a specific format, and to use the following format to crack it.
`[format]` - The format that the hash is in.

**Example** - 
```python
john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt
```

**A note on formats**:
When you are telling john to use formats, if you're dealing with a standard hash type, e.g. md5 as in the example above, you have to prefix it with `raw-` to tell john you're just dealing with a standard hash type, though this doesn't always apply. 

**To check if you need to add the prefix or not, you can list all of John's formats using the below one:**
```python
john --list=formats
```

**grep for your hash type using something like:**
```python
john --list=formats | grep -iF "md5"
```

### Cracking Windows Hashes
#### NTHash / NTLM
- NThash is the hash format that modern Windows Operating System machines will store user and service passwords in.
- It's also commonly referred to as "NTLM" which references the previous version of Windows format for hashing passwords known as "LM", thus "NT/LM".