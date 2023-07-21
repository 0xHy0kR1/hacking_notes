## Subfinder
### Steps
#### 1. Installing subfinder
```python
┌──(hyok㉿kali)-[~]
└─$ sudo apt install subfinder
```

#### 2. Help manu
```python
┌──(hyok㉿kali)-[~]
└─$ subfinder -h  
```

#### 3. Finding sub-domains related to domain
```python
┌──(hyok㉿kali)-[~]
└─$ subfinder -d tesla.com
____  _| |__ / _(_)_ _  __| |___ _ _ 
(_-< || | '_ \  _| | ' \/ _  / -_) '_|
/__/\_,_|_.__/_| |_|_||_\__,_\___|_| v2

		projectdiscovery.io

[WRN] Use with caution. You are responsible for your actions
[WRN] Developers assume no liability and are not responsible for any misuse or damage.
[WRN] By using subfinder, you also agree to the terms of the APIs used.

[INF] Configuration file saved to /home/hyok/.config/subfinder/config.yaml
[INF] Enumerating subdomains for tesla.com
origin-static-assets-pay.tesla.com
clsmdcfinp.tesla.com
partners.tesla.com
image-emails.tesla.com
energydesk.tesla.com
dataviz.tesla.com
--------------------------------SNIP-----------------------------------
```

## Certificate search for a domain(or sub-domain search)
![[certificate_search.png]]
- site --> [crt](https://crt.sh/)
- It also give you list of sub-domains related to domain that you input.

## Sub-domain finder bug bounty tool
### 1. Amass
#### Steps to install Amass
1. Install amass
```python
┌──(hyok㉿kali)-[~]
└─$ sudo apt-get install amass
[sudo] password for hyok: 
Reading package lists... Done
Building dependency tree... Done
```

2. Help menu in amass
```python
┌──(hyok㉿kali)-[~]
└─$ amass -h  
Subcommands: 

	amass intel - Discover targets for enumerations
	amass enum  - Perform enumerations and network mapping
	amass viz   - Visualize enumeration results
	amass track - Track differences between enumerations
	amass db    - Manipulate the Amass graph database
---------------------------------------SNIP------------------------------------
```

3. Help menu for amass intel
```python
┌──(hyok㉿kali)-[~]
└─$ amass intel -h
Usage: amass intel [options] [-whois -d DOMAIN] [-addr ADDR -asn ASN -cidr CIDR]

  -active
    	Attempt certificate name grabs
  -addr value
    	IPs and ranges (192.168.1.1-254) separated by commas
```

## Subdomains finding with assetfinder
![[sum-domain-assetfinder1.png]]

## Subdomains finding with amass
![[amass1.png]]

## Checking that host alive or not
**Checking host alive or not on port 80 and 443**
![[httprobe1.png]]

**Checking host alive or not only on port 443**
```python
┌──(kali㉿kali)-[~]
└─$ cat final.txt | httprobe -s -p https:443
```

**Stripped out the `https://` and `:443` from the output**
```python
┌──(kali㉿kali)-[~]
└─$ cat final.txt | httprobe -s -p https:443 | sed 's/https\?:\/\///' | tr -d ':443'
```

**Only displaying unique subdomains in the output**
```python
┌──(kali㉿kali)-[~]
└─$ cat final.txt | sort -u | httprobe -s -p https:443 | sed 's/https\?:\/\///' | tr -d ':443'
```

**Putting everything in the file**
```python
┌──(kali㉿kali)-[~]
└─$ cat final.txt | sort -u | httprobe -s -p https:443 | sed 's/https\?:\/\///' | tr -d ':443' >> final.txt
```

**Extracting content from the file**
```python
┌──(kali㉿kali)-[~]
└─$ cat final.txt | grep admin
```

## Taking screenshot with gowitness
**Command** - 
```python
gowitness single https://codewithharry.com
```
![[gowitness1.png]]
