## 1. Builtwith 
- it give us broad view of what are technologies used to built the website
- site --> [Builtwith](https://builtwith.com/)
![[builtwith.png]]

## 2. Wappalyzer
- It is same as Builtwith but it is a extension.
- site --> [wappalyzer](https://addons.mozilla.org/en-US/firefox/addon/wappalyzer/)
![[wappalyzer_extension.png]]
- Click on the above icon when do you visit any site, for info about that website.

## 3. whatweb
- WhatWeb identifies websites. It recognises web technologies including content management systems (CMS), blogging platforms, statistic/analytics packages, JavaScript libraries, web servers, and embedded devices.
- It is a built tool.

#### Example 
```python
┌──(hyok㉿kali)-[~]
└─$ whatweb https://tesla.com                                                                                  
https://tesla.com [403 Forbidden] Akamai-Global-Host, Country[UNITED STATES][US], HTTPServer[AkamaiGHost], IP[104.85.4.91], Strict-Transport-Security[max-age=15768000], Title[Access Denied], UncommonHeaders[x-reference-error,permissions-policy]
```
**Result** - It pulls out "ip address" but it can't pull more than that.