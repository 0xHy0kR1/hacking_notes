## There are two ways to search for NSE scripts:
1. The first is the page on the [Nmap website](https://nmap.org/nsedoc/)
2. The second is the local storage on your attacking machine. 

**Note** - Nmap stores its scripts on Linux at `/usr/share/nmap/scripts`.

## There are two ways to search for installed scripts:
1. One is by using the `/usr/share/nmap/scripts/script.db` file.
	It is a formatted text file containing filenames and categories for each available script.

2. The second way to search for scripts is quite simply to use the `ls` command

### 1. script.db file method for searching NSE scripts:
![[nmap6.png]]
1. we can also _grep_ through it to look for scripts:
![[nmap7.png]]

### 2. ls command to search for NSE scripts:
![[nmap8.png]]

### Seaching scripts on the basis of category:
![[nmap9.png]]

## Downloading a missing script:
```python
`sudo wget -O /usr/share/nmap/scripts/<script-name>.nse https://svn.nmap.org/nmap/scripts/<script-name>.nse`
```
**Followed by below: Updating the script.db**
```python
nmap --script-updatedb
```


