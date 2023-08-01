## Cracking a Password Protected Zip File
we're going to be using a separate part of the john suite of tools to convert the zip file into a format that John will understand. 

## Zip2John
we're going to be using the zip2john tool to convert the zip file into a hash format that John is able to understand.

#### Syntax - 
`zip2john [options] [zip file] > [output file]`

`[options]` - Allows you to pass specific checksum options to zip2john, this shouldn't often be necessary  

`[zip file]` - The path to the zip file you wish to get the hash of

`>` - This is the output director, we're using this to send the output from this file to the...

`[output file]` - This is the file that will store the output from

**Example Usage**
```python
zip2john zipfile.zip > zip_hash.txt
```

#### Cracking
We're then able to take the file we output from zip2john in our example use case called "zip_hash.txt".
feed it directly into John as we have made the input specifically for it.
```python
john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt
```

