OSINT   - So you were said that everything belonging to some company is inside the scope, and you want to figure out what this company actually owns.

The goal of this phase is to obtain all the **companies owned by the main company** and then all the **assets** of these companies.

**To do so, we are going to:**
   1. Find the acquisitions of the main company, this will give us the companies inside the scope.
   2. Find the ASN (if any) of each company, this will give us the IP ranges owned by each company.
   3. Use reverse whois lookups to search for other entries (organisation names, domains...) related to the first one (this can be done recursively)
   4. Use other techniques like shodan `org`and `ssl`filters to search for other assets (the `ssl` trick can be done recursively).

### Acquisitions

   - First of all, we need to know which **other companies are owned by the main company**. One option is to visit [https://www.crunchbase.com/](https://www.crunchbase.com), **search** for the **main company**, and **click** on "**acquisitions**". There you will see other companies acquired by the main one.
![[ex_recon1.png]]

   - Other option is to visit the **Wikipedia** page of the main company and search for **acquisitions**.
   - Ok, at this point you should know all the companies inside the scope. Lets figure out how to find their assets.

### ASNs

   - An autonomous system number (**ASN**) is a **unique number** assigned to an **autonomous system** (AS) by the **Internet Assigned Numbers Authority (IANA)**.
   - An **AS** consists of **blocks** of **IP addresses** which have a distinctly defined policy for accessing external networks and are administered by a single organisation but may be made up of several operators.
   - It's interesting to find if the **company have assigned any ASN** to find its **IP ranges.** It will be interested to perform a **vulnerability test** against all the **hosts** inside the **scope** and **look for domains** inside these IPs
   - You can **search** by company **name**, by **IP** or by **domain** in [**https://bgp.he.net/**](https://bgp.he.net)**.** **Depending on the region of the company this links could be useful to gather more data:** [**AFRINIC**](https://www.afrinic.net) **(Africa),** [**Arin**](https://www.arin.net/about/welcome/region/)**(North America),** [**APNIC**](https://www.apnic.net) **(Asia),** [**LACNIC**](https://www.lacnic.net) **(Latin America),** [**RIPE NCC**](https://www.ripe.net) **(Europe). Anyway, probably all the** useful information **(IP ranges and Whois)** appears already in the first link.

**In simple words** - 
1. **ASN (Autonomous System Number):** Unique number assigned to an organization's network.
    
2. **Purpose:** Helps identify IP address ranges controlled by the organization.
    
3. **Tools:** Use [https://bgp.he.net/](https://bgp.he.net/) or regional registries (e.g., ARIN, APNIC).
    
4. **Process:**
    
    - Search by company name, IP, or domain.
    - Gather IP ranges and Whois data.
    - Perform vulnerability tests on identified hosts.
5. **Automation with Amass:**
    
    - `amass intel -org tesla`
    - `amass intel -asn 8911,50313,394161`

**Note** - Also, [**BBOT**](https://github.com/blacklanternsecurity/bbot)**'s** subdomain enumeration automatically aggregates and summarizes ASNs at the end of the scan.
```sh
bbot -t tesla.com -f subdomain-enum
...
[INFO] bbot.modules.asn: +----------+---------------------+--------------+----------------+----------------------------+-----------+
[INFO] bbot.modules.asn: | AS394161 | 8.244.131.0/24      | 5            | TESLA          | Tesla Motors, Inc.         | US        |
[INFO] bbot.modules.asn: +----------+---------------------+--------------+----------------+----------------------------+-----------+
[INFO] bbot.modules.asn: | AS16509  | 54.148.0.0/15       | 4            | AMAZON-02      | Amazon.com, Inc.           | US        |
[INFO] bbot.modules.asn: +----------+---------------------+--------------+----------------+----------------------------+-----------+
[INFO] bbot.modules.asn: | AS394161 | 8.45.124.0/24       | 3            | TESLA          | Tesla Motors, Inc.         | US        |
[INFO] bbot.modules.asn: +----------+---------------------+--------------+----------------+----------------------------+-----------+
[INFO] bbot.modules.asn: | AS3356   | 8.32.0.0/12         | 1            | LEVEL3         | Level 3 Parent, LLC        | US        |
[INFO] bbot.modules.asn: +----------+---------------------+--------------+----------------+----------------------------+-----------+
[INFO] bbot.modules.asn: | AS3356   | 8.0.0.0/9           | 1            | LEVEL3         | Level 3 Parent, LLC        | US        |
[INFO] bbot.modules.asn: +----------+---------------------+--------------+----------------+----------------------------+-----------+
```
You can find the IP ranges of an organisation also using [http://asnlookup.com/](http://asnlookup.com) (it has free API). You can find the IP and ASN of a domain using [http://ipv4info.com/](http://ipv4info.com).

#### Looking for vulnerabilities
At this point we known **all the assets inside the scope**, so if you are allowed you could launch some **vulnerability scanner** (Nessus, OpenVAS) over all the hosts.

Also, you could launch some [**port scans**](/generic-methodologies-and-resources/pentesting-network#discovering-hosts-from-the-outside) **or use services like** shodan **to find** open ports and also look for running services.

**Also, It could be worth it to mention that you can also prepare some** default username **and** passwords **lists and try to** bruteforce services with [https://github.com/x90skysn3k/brutespray](https://github.com/x90skysn3k/brutespray).

### Domains
> We know all the companies inside the scope and their assets, it's time to find the domains inside the scope.

Please, note that in the following purposed techniques you can also find subdomains and that information shouldn't be underrated.

First of all you should look for the **main domain**(s) of each company. For example, for _Tesla Inc._ is going to be _tesla.com_.

### Reverse DNS
- As you have found all the IP ranges of the domains you could try to perform **reverse dns lookups** on those **IPs to find more domains inside the scope**.

>Try to use some dns server of the victim or some well-known dns server (1.1.1.1, 8.8.8.8)
```sh
dnsrecon -r <DNS Range> -n <IP_DNS>   #DNS reverse of all of the addresses
dnsrecon -d facebook.com -r 157.240.221.35/24 #Using facebooks dns
dnsrecon -r 157.240.221.35/24 -n 1.1.1.1 #Using cloudflares dns
dnsrecon -r 157.240.221.35/24 -n 8.8.8.8 #Using google dns
```
For this to work, the administrator has to enable manually the PTR. You can also use a online tool for this info: [http://ptrarchive.com/](http://ptrarchive.com)

### Reverse Whois (loop)
- Inside a **whois** you can find a lot of interesting **information** like **organisation name**, **address**, **emails**, phone numbers...
- But which is even more interesting is that you can find **more assets related to the company** if you perform **reverse whois lookups by any of those fields** (for example other whois registries where the same email appears).
- You can use online tools like:
	- [https://viewdns.info/reversewhois/](https://viewdns.info/reversewhois/) - **Free**
	- [https://domaineye.com/reverse-whois](https://domaineye.com/reverse-whois) - **Free**
	- [https://www.reversewhois.io/](https://www.reversewhois.io) - **Free**
	- [https://www.whoxy.com/](https://www.whoxy.com) - **Free** web, not free API.
	- [http://reversewhois.domaintools.com/](http://reversewhois.domaintools.com) - Not free
	- [https://drs.whoisxmlapi.com/reverse-whois-search](https://drs.whoisxmlapi.com/reverse-whois-search) - Not Free (only **100 free** searches)
	- [https://www.domainiq.com/](https://www.domainiq.com) - Not Free

- You can automate this task using [**DomLink**](https://github.com/vysecurity/DomLink) (requires a whoxy API key).
- You can also perform some automatic reverse whois discovery with [amass](https://github.com/OWASP/Amass): `amass intel -d tesla.com -whois`
- Note that you can use this technique to discover more domain names every time you find a new domain.

### Trackers
- If find the **same ID of the same tracker** in 2 different pages you can suppose that **both pages** are **managed by the same team**. For example, if you see the same **Google Analytics ID** or the same **Adsense ID** on several pages.
- There are some pages and tools that let you search by these trackers and more:
	- [**Udon**](https://github.com/dhn/udon)
	- [**BuiltWith**](https://builtwith.com)
	- [**Sitesleuth**](https://www.sitesleuth.io)
    - [**Publicwww**](https://publicwww.com)
	- [**SpyOnWeb**](http://spyonweb.com)

### Favicon
Did you know that we can find related domains and sub domains to our target by looking for the same favicon icon hash? This is exactly what [favihash.py](https://github.com/m4ll0k/Bug-Bounty-Toolz/blob/master/favihash.py) tool made by [@m4ll0k2](https://twitter.com/m4ll0k2) does. Here’s how to use it:
```sh
cat my_targets.txt | xargs -I %% bash -c 'echo "http://%%/favicon.ico"' > targets.txt
python3 favihash.py -f https://target/favicon.ico -t targets.txt -s
```

![[assetd1.jpg]]
favihash - discover domains with the same favicon icon hash

Simply said, favihash will allow us to discover domains that have the same favicon icon hash as our target.
Moreover, you can also search technologies using the favicon hash as explained in [**this blog post**](https://medium.com/@Asm0d3us/weaponizing-favicon-ico-for-bugbounties-osint-and-what-not-ace3c214e139). That means that if you know the **hash of the favicon of a vulnerable version of a web tech** you can search if in shodan and **find more vulnerable places**:
```sh
shodan search org:"Target" http.favicon.hash:116323821 --fields ip_str,port --separator " " | awk '{print $1":"$2}'
```

**This is how you can **calculate the favicon hash** of a web:**
```python
import mmh3
import requests
import codecs

def fav_hash(url):
    response = requests.get(url)
    favicon = codecs.encode(response.content,"base64")
    fhash = mmh3.hash(favicon)
    print(f"{url} : {fhash}")
    return fhash
```

### Copyright / Uniq string
Search inside the web pages **strings that could be shared across different webs in the same organisation**. The **copyright string** could be a good example. Then search for that string in **google**, in other **browsers** or even in **shodan**: `shodan search http.html:"Copyright string"`

### CRT Time
The given cron job, typically found in the /etc/crontab file, is used to automatically renew all the domain certificates on a server. It runs the 'certbot renew' command every 10 days at 1:37 PM. After renewal, it reloads the Nginx web server using 'systemctl reload nginx
```sh
# /etc/crontab
37 13 */10 * * certbot renew --post-hook "systemctl reload nginx"
```
This setup helps ensure that even if the Certificate Authority (CA) doesn't include the generation time in the certificate's validity period, one can still identify domains owned by the same company by checking certificate transparency logs. 

For more details, you can refer to the provided [**writeup for more information**](https://swarm.ptsecurity.com/discovering-domains-via-a-time-correlation-attack/).

### Passive Takeover
- People often associate subdomains with cloud provider IPs, and sometimes they lose the IP but forget to remove the DNS record.
- By simply creating a VM on a cloud platform like Digital Ocean, you might inadvertently acquire control over some subdomains.
- [**This post**](https://kmsec.uk/blog/passive-takeover/) shares a story about this situation and suggests a script. The script creates a VM on Digital Ocean, retrieves the new machine's IPv4 address, and searches Virustotal for subdomain records pointing to it.

### Other ways
Note that you can use this technique to discover more domain names every time you find a new domain.

### Shodan
- As you're aware of the organization owning the IP space, use Shodan to search with the command: `org:"Tesla, Inc."`. Examine the discovered hosts for any unexpected domains listed in the TLS certificates.
- You could access the **TLS certificate** of the main web page, obtain the **Organisation name** and then search for that name inside the **TLS certificates** of all the web pages known by **shodan** with the filter : `ssl:"Tesla Motors"` or use a tool like [**sslsearch**](https://github.com/HarshVaragiya/sslsearch).

### Assetfinder
- [**Assetfinder**](https://github.com/tomnomnom/assetfinder) is a tool that look for **domains related** with a main domain and **subdomains** of them.

### Looking for vulnerabilities
- Search for potential domain takeover opportunities. If a company has lost ownership of a domain, consider registering it at a low cost and informing the company.
- If you find any **domain with an IP different** from the ones you already found in the assets discovery, you should perform a **basic vulnerability scan** (using Nessus or OpenVAS) and some [**port scan**](/generic-methodologies-and-resources/pentesting-network#discovering-hosts-from-the-outside) with **nmap/masscan/shodan**.

## Subdomains
> We know all the companies inside the scope, all the assets of each company and all the domains related to the companies.

It's time to find all the possible subdomains of each found domain.

### DNS
>Let's try to get **subdomains** from the **DNS** records. We should also try for **Zone Transfer** (If vulnerable, you should report it).
```sh
dnsrecon -a -d tesla.com
```

## OSINT
- The fastest way to obtain a lot of subdomains is search in external sources. The most used **tools** are the following ones (for better results configure the API keys):

### [**BBOT**](https://github.com/blacklanternsecurity/bbot)
```sh
# subdomains
bbot -t tesla.com -f subdomain-enum

# subdomains (passive only)
bbot -t tesla.com -f subdomain-enum -rf passive

# subdomains + port scan + web screenshots
bbot -t tesla.com -f subdomain-enum -m naabu gowitness -n my_scan -o .
```

### [**Amass**](https://github.com/OWASP/Amass)
```sh
amass enum [-active] [-ip] -d tesla.com
amass enum -d tesla.com | grep tesla.com # To just list subdomains
```

### [**subfinder**](https://github.com/projectdiscovery/subfinder)
```sh
# Subfinder, use -silent to only have subdomains in the output
./subfinder-linux-amd64 -d tesla.com [-silent]
```

### [**findomain**](https://github.com/Edu4rdSHL/findomain/)
```sh
# Subfinder, use -silent to only have subdomains in the output
./subfinder-linux-amd64 -d tesla.com [-silent]
```

### [**OneForAll**](https://github.com/shmilylty/OneForAll/tree/master/docs/en-us)
```sh
python3 oneforall.py --target tesla.com [--dns False] [--req False] [--brute False] run
```

### [**assetfinder**](https://github.com/tomnomnom/assetfinder)
```sh
assetfinder --subs-only <domain>
```

### [**Sudomy**](https://github.com/Screetsec/Sudomy)
```sh
# It requires that you create a sudomy.api file with API keys
sudomy -d tesla.com
```

### [**vita**](https://github.com/junnlikestea/vita)
```sh
vita -d tesla.com
```

### [**theHarvester**](https://github.com/laramies/theHarvester)
```sh
theHarvester -d tesla.com -b "anubis, baidu, bing, binaryedge, bingapi, bufferoverun, censys, certspotter, crtsh, dnsdumpster, duckduckgo, fullhunt, github-code, google, hackertarget, hunter, intelx, linkedin, linkedin_links, n45ht, omnisint, otx, pentesttools, projectdiscovery, qwant, rapiddns, rocketreach, securityTrails, spyse, sublist3r, threatcrowd, threatminer, trello, twitter, urlscan, virustotal, yahoo, zoomeye"
```

**There are **other interesting tools/APIs** that even if not directly specialised in finding subdomains could be useful to find subdomains, like:**
### [**Crobat**](https://github.com/cgboal/sonarsearch)
- Uses the API [https://sonar.omnisint.io](https://sonar.omnisint.io) to obtain subdomains
```sh
# Get list of subdomains in output from the API
## This is the API the crobat tool will use
curl https://sonar.omnisint.io/subdomains/tesla.com | jq -r ".[]"
```

### [**JLDC free API**](https://jldc.me/anubis/subdomains/google.com)
```sh
curl https://jldc.me/anubis/subdomains/tesla.com | jq -r ".[]"
```

### [**RapidDNS**](https://rapiddns.io) free API
```sh
# Get Domains from rapiddns free API
rapiddns(){
 curl -s "https://rapiddns.io/subdomain/$1?full=1" \
  | grep -oE "[\.a-zA-Z0-9-]+\.$1" \
  | sort -u
}
rapiddns tesla.com
```

### ​[**https://crt.sh/**](https://crt.sh/)
```sh
# Get Domains from crt free API
crt(){
 curl -s "https://crt.sh/?q=%25.$1" \
  | grep -oE "[\.a-zA-Z0-9-]+\.$1" \
  | sort -u
}
crt tesla.com
```

### [**gau**](https://github.com/lc/gau)
- fetches known URLs from AlienVault's Open Threat Exchange, the Wayback Machine, and Common Crawl for any given domain.
```sh
# Get subdomains from GAUs found URLs
gau --subs tesla.com | cut -d "/" -f 3 | sort -u
```

### [**SubDomainizer**](https://github.com/nsonaniya2010/SubDomainizer) **&** [**subscraper**](https://github.com/Cillian-Collins/subscraper)
- They search the internet for JS files and retrieve subdomains from them.
```sh
# Get only subdomains from SubDomainizer
python3 SubDomainizer.py -u https://tesla.com | grep tesla.com

# Get only subdomains from subscraper, this already perform recursion over the found results
python subscraper.py -u tesla.com | grep tesla.com | cut -d " " -f
```

### ​[**Shodan**](https://www.shodan.io/)
```sh
# Get info about the domain
shodan domain <domain>
# Get other pages with links to subdomains
shodan search "http.html:help.domain.com"
```

### [**Censys subdomain finder**](https://github.com/christophetd/censys-subdomain-finder)
```sh
export CENSYS_API_ID=...
export CENSYS_API_SECRET=...
python3 censys-subdomain-finder.py tesla.com
```

### ​[**DomainTrail.py**](https://github.com/gatete/DomainTrail)
```sh
python3 DomainTrail.py -d example.com
```

- [**securitytrails.com**](https://securitytrails.com/) has a free API to search for subdomains and IP history
- [**chaos.projectdiscovery.io**](https://chaos.projectdiscovery.io/#/)

## DNS Brute force

Let's discover additional subdomains by systematically checking DNS servers with various potential subdomain names.

**For this action you will need some common subdomains wordlists like**:
- [https://gist.github.com/jhaddix/86a06c5dc309d08580a018c66354a056](https://gist.github.com/jhaddix/86a06c5dc309d08580a018c66354a056)
- [https://wordlists-cdn.assetnote.io/data/manual/best-dns-wordlist.txt](https://wordlists-cdn.assetnote.io/data/manual/best-dns-wordlist.txt)
- [https://localdomain.pw/subdomain-bruteforce-list/all.txt.zip](https://localdomain.pw/subdomain-bruteforce-list/all.txt.zip)
- [https://github.com/pentester-io/commonspeak](https://github.com/pentester-io/commonspeak)
- [https://github.com/danielmiessler/SecLists/tree/master/Discovery/DNS](https://github.com/danielmiessler/SecLists/tree/master/Discovery/DNS)

And also IPs of good DNS resolvers. In order to generate a list of trusted DNS resolvers you can download the resolvers from [https://public-dns.info/nameservers-all.txt](https://public-dns.info/nameservers-all.txt) and use [**dnsvalidator**](https://github.com/vortexau/dnsvalidator) to filter them. Or you could use: [https://raw.githubusercontent.com/trickest/resolvers/main/resolvers-trusted.txt](https://raw.githubusercontent.com/trickest/resolvers/main/resolvers-trusted.txt)

**The most recommended tools for DNS brute-force are:**
1. [**massdns**](https://github.com/blechschmidt/massdns): This was the first tool that performed an effective DNS brute-force. It's very fast however it's prone to false positives.
```sh
sed 's/$/.domain.com/' subdomains.txt > bf-subdomains.txt
./massdns -r resolvers.txt -w /tmp/results.txt bf-subdomains.txt
grep -E "tesla.com. [0-9]+ IN A .+" /tmp/results.txt
```

1. [**gobuster**](https://github.com/OJ/gobuster): This one I think just uses 1 resolver
```sh
gobuster dns -d mysite.com -t 50 -w subdomains.txt
```

2. [**shuffledns**](https://github.com/projectdiscovery/shuffledns) is a wrapper around `massdns`, written in go, that allows you to enumerate valid subdomains using active bruteforce, as well as resolve subdomains with wildcard handling and easy input-output support.
```sh
shuffledns -d example.com -list example-subdomains.txt -r resolvers.txt
```

3. [**puredns**](https://github.com/d3mondev/puredns): It also uses `massdns`.
```sh
puredns bruteforce all.txt domain.com
```

4. [**aiodnsbrute**](https://github.com/blark/aiodnsbrute) uses asyncio to brute force domain names asynchronously.
```sh
aiodnsbrute -r resolvers -w wordlist.txt -vv -t 1024 domain.com
```

## Second DNS Brute-Force Round
- After having found subdomains using open sources and brute-forcing, you could generate alterations of the subdomains found to try to find even more. Several tools are useful for this purpose:

1. [**dnsgen**](https://github.com/ProjectAnte/dnsgen)**:** Given the domains and subdomains generate permutations.
```sh
cat subdomains.txt | dnsgen -
```

2. [**goaltdns**](https://github.com/subfinder/goaltdns): Given the domains and subdomains generate permutations.
- You can get goaltdns permutations **wordlist** in [**here**](https://github.com/subfinder/goaltdns/blob/master/words.txt).
```sh
goaltdns -l subdomains.txt -w /tmp/words-permutations.txt -o /tmp/final-words-s3.txt
```

3. [**gotator**](https://github.com/Josue87/gotator)**:** Given the domains and subdomains generate permutations. If not permutations file is indicated gotator will use its own one.
```sh
gotator -sub subdomains.txt -silent [-perm /tmp/words-permutations.txt]
```

4. [**altdns**](https://github.com/infosec-au/altdns): Apart from generating subdomains permutations, it can also try to resolve them (but it's better to use the previous commented tools).
- You can get altdns permutations **wordlist** in [**here**](https://github.com/infosec-au/altdns/blob/master/words.txt).
```sh
altdns -i subdomains.txt -w /tmp/words-permutations.txt -o /tmp/asd3
```

5. [**dmut**](https://github.com/bp0lr/dmut): Another tool to perform permutations, mutations and alteration of subdomains. This tool will brute force the result (it doesn't support dns wild card).
- You can get dmut permutations wordlist in [**here**](https://raw.githubusercontent.com/bp0lr/dmut/main/words.txt).
```sh
cat subdomains.txt | dmut -d /tmp/words-permutations.txt -w 100 \
    --dns-errorLimit 10 --use-pb --verbose -s /tmp/resolvers-trusted.txt
```

6. [**alterx**](https://github.com/projectdiscovery/alterx): It creates possible subdomain names by analyzing a domain and applying specified patterns in an attempt to uncover additional subdomains.

