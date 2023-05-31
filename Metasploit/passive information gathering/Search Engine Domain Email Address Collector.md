- The Search Engine Domain Email Address Collector module in Metasploit is a tool that utilizes search engines such as Google, Bing, and Yahoo to gather a list of valid email addresses associated with a specific target domain.
-  The resulting list of email addresses can be useful for identifying potential targets for social engineering.
# Code - 
```python
msf6 auxiliary(gather/shodan_honeyscore) > use auxiliary/gather/search_email_collector
msf6 auxiliary(gather/search_email_collector) > set DOMAIN linkedin.com
DOMAIN => linkedin.com
msf6 auxiliary(gather/search_email_collector) > run

[*] Harvesting emails .....
[*] Searching Google for email addresses from linkedin.com
[*] Extracting emails from Google search results...
[*] Searching Bing email addresses from linkedin.com
[*] Extracting emails from Bing search results...
[*] Searching Yahoo for email addresses from linkedin.com
[*] Extracting emails from Yahoo search results...
[*] Located 0 email addresses for linkedin.com
[*] Auxiliary module execution completed
```