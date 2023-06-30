## robots.txt
The robots.txt file is a document that tells search engines which pages they are and aren't allowed to show on their search engine results or ban specific search engines from crawling the website altogether.

## Favicon
The favicon is a small icon displayed in the browser's address bar or tab used for branding a website.
![[web_terms1.png]]

Sometimes when frameworks are used to build a website, a favicon that is part of the installation gets leftover, and if the website developer doesn't replace this with a custom one, this can give us a clue on what framework is in use.

common framework icons -->  [https://wiki.owasp.org/index.php/OWASP_favicon_database](https://wiki.owasp.org/index.php/OWASP_favicon_database)

#### Downloading the favicon of website:
command --> 
```python
curl https://static-labs.tryhackme.cloud/sites/favicon/images/favicon.ico | md5sum
```
![[web_terms2.png]]

**Searching the framework that used to make this website using above hash**
![[web_terms3.png]]

## sitemap.xml
the sitemap.xml file gives a list of every file the website owner wishes to be listed on a search engine.

## HTTP header details using curl:
![[web_terms4.png]]

