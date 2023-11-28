
### 1. Google

   - Google is as good a place as any to start a search, but sometimes it can be of surprisingly limited value for finding e-mail addresses. The main reason for this is that the places where people use their e-mail addresses (such as account login pages) are not accessible to Google.

>**Use quotation marks to return exact matches only. Searching for "user@domain.com" is more precise than searching for just `user@domain.com`.**
```
"user@domain.com"
```



>**The "intext" search modifier can also be used to find webpages where the e-mail address appears as a string.**
```
site:targetcompany intext:target@email.com
```
This can be particularly effective when combined with the site: modifier to search within the website of a company that your target is associated to.

>**You could even tweak this technique to find a whole host of e-mail addresses associated to your target’s organisation with the following search term**
```
site:organisation.com intext:@organisation.com
```
This would return all indexable e-mail addresses within the company’s website.


**Example** - 
```
site:bbc.co.uk intext:@bbc.co.uk
```
You can use the above query to find all the e-mail addresses listed within the **bbc.co.uk** domain.


>**Use the "filetype:" search operator to find where your target’s e-mail address.**
```
intext:”boris.johnson.mp@parliament.uk” filetype:pdf
```
   - This will find any PDFs containing Boris Johnson’s parliamentary e-mail address.
   - This can find a target’s e-mail address hidden away inside PDF or other file types.
   - This can reveal company documents, invoices, meeting minutes, sports club fixtures or any other kind of document.
   - It’s particularly effective when searching for e-mails linked to organisations that have a lot of documents available on the web, such as government institutions or universities.

**Note** - It’s also worth mentioning [FaganFinder](https://www.faganfinder.com/filetype/) at this point. It works in a similar way to the Google filetype: search but it allows to combine different file types with a wider range of search engines.

### 2. Username

   - There’s often a link between someone’s e-mail address and their usernames. A good technique to try is to take the first part of a subject’s e-mail address and run it  through a number of username search engines and but the best tool for this is Sherlock.
   ![[email_osint1.png]]

### 3. Pastes

   Pastes are a treasure trove of OSINT information. They contain data breaches, public records, chatroom logs, and dozens of other kinds of useful information – including e-mail addresses. [Pastebin](https://pastebin.com) is by far the most widely-used and has its own built in search engine.

![[email_osint2.png]]