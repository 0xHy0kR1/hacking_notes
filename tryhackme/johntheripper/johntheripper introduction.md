## Introduction

### What are Hashes?
- A hash is a way of taking a piece of data of any length and  representing it in another form that is a fixed length. This is done by running the original data through a hashing algorithm.
- There are many popular hashing algorithms, such as MD4,MD5, SHA1 and NTLM.

### What makes Hashes secure?
- Hashing algorithms are designed so that they only operate one way. This means that a calculated hash cannot be reversed using just the output given.

### Where John Comes in...
If you have the hashed version of a password, and you know the hashing algorithm- you can use that hashing algorithm to hash a large number of words, called a dictionary.
You can then compare these hashes to the one you're trying to crack, to see if any of them match.
If they do, you now know what word corresponds to that hash- you've cracked it!
**This process is a dictionary attack.**

### syntax 
```python
john [options] [path to file]
```
`john` - Invokes the John the Ripper program
`[path to file]` - The file containing the hash you're trying to crack, if it's in the same directory you won't need to name a path, just the file.

