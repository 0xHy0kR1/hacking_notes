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

#### There are several modes of cracking you can use:
   - **Wordlist mode** - In which consist in trying all words contained in a dictionary. For example, a list of common passwords, a list of usernames, etc.
   - **Incremental mode** - which consist in trying all possible character combinations as passwords. This is powerful but much more longer especially if the password is long.
   - **Rule mode** - which consist in using the wordlist mode by adding it some pattern or mangle the string. For example adding the current year, or appending a common special character.

**There are 2 ways of performing a rule based bruteforce:**

1. Generating a custom wordlist and using the classic wordlist mode with it.  
    
2. Using a common wordlist and tell the cracking tool to apply some custom mangling rules on it.

**John the Ripper already include various mangling rules but you can create your owns and apply them the wordlist when cracking:**
```python
$ john hash.txt --wordlist=/usr/share/wordlists/passwords/rockyou.txt rules=norajCommon02
```

#### mutation rules
- **Border mutation** - commonly used combinations of digits and special symbols can be added at the end or at the beginning, or both
- **Freak mutation** - letters are replaced with similarly looking special symbols  
    
- **Case mutation** - the program checks all variations of uppercase/lowercase letters for any character
- **Order mutation** - character order is reversed
- **Repetition mutation** - the same group of characters are repeated several times
- **Vowels mutation** - vowels are omitted or capitalized
- **Strip mutation** - one or several characters are removed
- **Swap mutation** - some characters are swapped and change places
- **Duplicate mutation** - some characters are duplicated
- **Delimiter mutation** - delimiters are added between characters


### syntax 
```python
john [options] [path to file]
```
`john` - Invokes the John the Ripper program
`[path to file]` - The file containing the hash you're trying to crack, if it's in the same directory you won't need to name a path, just the file.

