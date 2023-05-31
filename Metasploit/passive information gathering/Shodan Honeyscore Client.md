- Checking whether a server is a honeypot or not is always a good idea.
- The last thing you want is to waste your time or be blocked because you were trying to attack a honeypot.
- Using the Shodan Honeyscore Client auxiliary module, you can use Shodan to check whether a server is a honeypot or not. The API returns a score from 0.0 to 1.0, 1.0 being a honeypot:
# Code - 
```python
msf6 > use auxiliary/gather/shodan_honeyscore
msf6 auxiliary(gather/shodan_honeyscore) > set SHODAN_APIKEY 9ibx02XQ0JlPYSK9CCRlm43M6B5ZZ5I8
SHODAN_APIKEY => 9ibx02XQ0JlPYSK9CCRlm43M6B5ZZ5I8
msf6 auxiliary(gather/shodan_honeyscore) > set TARGET 192.168.1.9
TARGET => 192.168.1.9
msf6 auxiliary(gather/shodan_honeyscore) > run
```
## Some extra information -
- You can also check whether a server honeypot or not by going there and typing the ip of server --> https://honeyscore.shodan.io/