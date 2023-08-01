## Cracking a Password Protected RAR Archive
rar archives are compressed files created by the Winrar archive manager. Just like zip files they compress a wide variety of folders and files.

## Rar2John
we're going to use the rar2john tool to convert the rar file into a hash format that John is able to understand.

#### Syntax
```python
rar2john [rar file] > [output file]
```

`rar2john` - Invokes the rar2john tool

`[rar file]` - The path to the rar file you wish to get the hash of

`>` - This is the output director, we're using this to send the output from this file to the...  

`[output file]` - This is the file that will store the output from

**Example** - 
```python
rar2john rarfile.rar > rar_hash.txt
```

## Cracking
we're then able to take the file we output from rar2john in our example use case called "rar_hash.txt" and feed it directly into John.
```python
john --wordlist=/usr/share/wordlists/rockyou.txt rar_hash.txt
```

