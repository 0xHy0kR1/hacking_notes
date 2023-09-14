## wordlistctl - 
It is a script to fetch, install, update and search wordlist archives from websites offering wordlists with more than 6300 wordlists available.

path - /opt/wordlistctl

##### To search for this wordlist with wordlistclt run:
```python
/opt/wordlistctl/wordlistctl.py search rockyou
```

##### Download and install rockyou wordlist by running this command:
```python
wordlistctl fetch -l rockyou
```

##### Now search again for rockyou on your local archive
![[external_tools1.png]]

##### Decompressing compressed wordlists
```python
wordlistctl fetch -l rockyou -d
```

##### Searching for a wordlist about a specific subject (eg. facebook):
```python
wordlistctl search facebook
```

##### Fetching the dogs.txt
```python
sudo ./wordlistctl.py fetch -l dogs -d /usr/share/wordlists/misc/dogs.txt
```

![[external_tools2.png]]

##### List out the wordlist in the usernames category
![[external_tools3.png]]

## Haiti - 
[Haiti](https://noraj.github.io/haiti/) is a CLI tool to identify the hash type of a given hash. [Install](https://noraj.github.io/haiti/#/pages/install) it.

## Mentalist - 
visit --> https://m.twitch.tv/videos/1510083151 or https://shamsher-khan-404.medium.com/crack-the-hash-level-2-tryhackme-writeup-292c86b72ea0 or https://tryhackme.com/room/crackthehashlevel2
to learn about mentalist

## Cewl
  It is used to generate a wordlist from a website. It could be useful to retrieve a lot of words related to the password's topic.

##### To download all words from example.org with a depth of 2, run:
```python
cewl -d 2 -w $(pwd)/example.txt https://example.org
```
The depth is the number of link level the spider will follow.

## ttpassgen

1. With [TTPassGen](https://github.com/tp7309/TTPassGen) we can craft wordlists from scratch. Create a first wordlist containing all 4 digits PIN code value.
```python
ttpassgen --rule '[?d]{4:4:*}' pin.txt
```

2. Generate a list of all lowercase chars combinations of length 1 to 3.
```python
ttpassgen --rule '[?l]{1:3:*}' abc.txt
```

3. Then we can create a new wordlist that is a combination of several wordlists. Eg. combine the PIN wordlist and the letter wordlist separated by a dash.
```python
ttpassgen --dictlist 'pin.txt,abc.txt' --rule '$0[-]{1}$1' combination.txt
```

