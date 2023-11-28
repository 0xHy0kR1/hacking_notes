## What is google dorking?
The term ‘Google dorks’ has been around for quite some years by now and is used for specific search queries that use Google’s search operators, combined with targeted parameters to find specific information.

## Google dorks based on the type of target:

### People and Accounts

>**finding the emails based on a username**
```
username*com
```
Instead of searching for all possible email providers, we replaced the domain name with an asterisk:


>**It searches for online resumes of a person.**
```
inurl:resume “john smith”
intext:resume “john smith”
```
You can search within the URL of a website, or within the text of a site:

>**Finding emails**
```
“user@domain.com”
```

**Note** - Use quotation marks to return exact matches only. Searching for `user@domain.com` is more precise than searching for just `user@domain.com`.


>**By targeting the LinkedIn site, he searches for people with a specific job title and location**
```
site:http://linkedin.com/in "<job title>" (☎ OR ☏ OR ✆ OR 📱) +"<location>"
```
But he shared another trick, which is the fact that you can search for icons or Unicode characters:


>**And in case you are looking for a specific name, you can of course always search for:**
```
"<name>" (☎ OR ☏ OR ✆ OR 📱)
```


>**finding people within GitHub code:**
```
site:http://github.com/orgs/*/people
```


>**if you are looking for lists of attendees, or finalists, you can try the below dork:**
```
intitle:final.attendee.list OR inurl:final.attendee.list
```


>**It searches for login information on a Trello board**
```
site:http://trello.com password + admin OR username
```
Since a lot of people forget to tighten the security settings on their Trello board, loads of them are exposed and indexed by Google:


>**This would return all indexable e-mail addresses within the company’s website**
```
site:organisation.com intext:@organisation.com
```
Example --> `site:bbc.co.uk intext:@bbc.co.uk`


### Documents

>**To finding specific documents within a website or domain name, Google dork to do just that:**
```
site:<domain> filetype:PDF
```
Instead of ‘filetype:’ you can also use the abbreviation for extention, which is: ‘ext:’


>**A search that is also targeting PDF’s, but it shows how to search for only those documents that might contain possible email information.**
```
filetype:pdf <domain> "email"
```
Change the `<domain>` to the specific company domain name and have a look what’s out there:


>**A dork that is looking for XLS files within government websites:**
```
filetype:xls site:.gov
```


>**A dork that is looking not only for XLS files but also for many files within government websites:**
```
filetype:"xls | xlsx | doc | docx | txt | pdf" site:.gov
```

OR

```
filetype:"doc | pdf | xls | txt | ps | rtf | odt | sxw | psw | ppt | pps | xml" site:.gov
```


>**searching for any kind of document on HubSpot that contains the word ‘trends’ and that has the year 2019 in the URL:**
```
site:http://cdn2.hubspot.net intitle:2019 OR inurl:2019 "* trends"
```


>**A Dork that targeting Google as email platform with looking for txt OR pdf files containing words like FBI, CIA Or NYpD (these are interchangeable by words by your particular interest):
```
"Email delivery powered by Google" ext:pdf OR ext:txt nypd OR fbi OR cia
```


### Cloud, Buckets and Databases

>**This one is searching for indexed documents that contain the phrase ‘confidential’ or ‘top secret’ within open Amazon S3 buckets:**
```
site:http://s3.amazonaws.com confidential OR "top secret"
```


>**The below dork show some confidential login information within XLS files:**
```
s3 site:http://amazonaws.com filetype:xls password
```


>**You can search for copies of databases via Google too. To find some of them, simply search for:**
```
ext:sql intext:"-- phpMyAdmin SQL Dump"
```


### Social Media

>**How to find out whether a certain tweet was shared on other media, for instance a news site. For that, search for the specific text and tell Google to ignore anything that was posted within twitter.com by adding the minus sign to that part of the dork:**
```
"text of a tweet" -site:https://twitter.com
```
Almost the same method can be used to search messages and/or links for a specific username not coming from that username his/her account.


>For example this searches for links or information containing ‘@dutch_osintguy’ but not coming directly of the twitter user timeline Dutch_osintguy
```
@dutch_osintguy -site:twitter.com/dutch_osintguy
```


**NOTE** - _Google has limited the amount of keywords that you can search for to a total of 32 words. This means that all search term beyond the 32 word limit will not be taken into account (keyword 33 and beyond) in a search._

Best google dork sites --> [google_guide](https://www.googleguide.com/advanced_operators_reference.html) and [exploit-db](https://www.exploit-db.com/google-hacking-database)
