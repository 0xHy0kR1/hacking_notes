## Introduction
- LFI attacks against web applications are often due to a developers' lack of security awareness. With PHP, using functions such as include, require, include_once, and require_once often contribute to vulnerable web applications.
- LFI vulnerabilities also occur when using other languages such as ASP, JSP, or even in Node.js apps.

### we will walk you through various LFI scenarios and how to exploit them
1. Suppose the web application provides two languages, and the user can select between the EN and AR
```php
<?PHP 
	include($_GET["lang"]);
?>
```
- The PHP code above uses a GET request via the URL parameter lang to include the file of the page.
- The call can be done by sending the following HTTP request as follows: http://webapp.thm/index.php?lang=EN.php[](http://webapp.thm/index.php?lang=EN.php) to load the English page or http://webapp.thm/index.php?lang=AR.php to load the Arabic page, where EN.php and AR.php files exist in the same directory.
- Let's say we want to read the /etc/passwd file, which contains sensitive information about the users of the Linux operating system, we can try the following: http://webapp.thm/get.php?file=/etc/passwd
- In this case, it works because there isn't a directory specified in the include function and no input validation.

2. Next, In the following code, the developer decided to specify the directory inside the function.
```php
<?PHP 
	include("languages/". $_GET['lang']); 
?>
```
- In the above code, the developer decided to use the include function to call PHP pages in the languages directory only via lang parameters.
- If there is no input validation, the attacker can manipulate the URL by replacing the lang input with other OS-sensitive files such as /etc/passwd.
- Again the payload looks similar to the path traversal, but the include function allows us to include any called files into the current page. The following will be the exploit:
```php
http://webapp.thm/index.php?lang=../../../../etc/passwd
```

## Scenario-2
- In this scenario, we have the following entry point: http://webapp.thm/index.php?lang=EN. If we enter an invalid input, such as THM, we get the following error.
```php
Warning: include(languages/THM.php): failed to open stream: No such file or directory in /var/www/html/THM-4/index.php on line 12
```
- The error message discloses significant information. By entering THM as input, an error message shows what the include function looks like:  include(languages/THM.php);.
**Note** - If you look at the directory closely, we can tell the function includes files in the languages directory is adding  .php at the end of the entry.

1. To exploit this, we need to use the ../ trick, as described in the directory traversal section, to get out the current folder. Let's try the following:
```php
http://webapp.thm/index.php?lang=../../../../etc/passwd
```

2. Note that we used 4 ../ because we know the path has four levels /var/www/html/THM-4. But we still receive the following error:
```php
Warning: include(languages/../../../../../etc/passwd.php): failed to open stream: No such file or directory in /var/www/html/THM-4/index.php on line 12
```
It seems we could move out of the PHP directory but still, the include function reads the input with .php at the end! This tells us that the developer specifies the file type to pass to the include function.

3. To bypass this scenario, we can use the NULL BYTE, which is %00.
- Using null bytes is an injection technique where URL-encoded representation such as %00 or 0x00 in hex with user-supplied data to terminate strings. You could think of it as trying to trick the web app into disregarding whatever comes after the Null Byte.

4. By adding the Null Byte at the end of the payload, we tell the  include function to ignore anything after the null byte which may look like:
```php
include("languages/../../../../../etc/passwd%00").".php"); which equivalent to → include("languages/../../../../../etc/passwd");
```
**NOTE: the %00 trick is fixed and not working with PHP 5.3.4 and above.**
![[file_inclusion7.png]]

## Scenario-3
** In this section, the developer decided to filter keywords to avoid disclosing sensitive information! The /etc/passwd file is being filtered.**
#### There are two possible methods to bypass the filter:
1. First, by using the NullByte %00.
The exploit will be similar to http://webapp.thm/index.php?lang=/etc/passwd%00.

2. the current directory trick at the end of the filtered keyword `/.`
The exploit will be similar to http://webapp.thm/index.php?lang=/etc/passwd/.

**Second step in simple terms** - 
- To make it clearer, if we try this concept in the file system using cd .., it will get you back one step; however, if you do cd ., It stays in the current directory.
- Similarly, if we try  /etc/passwd/.., it results to be  /etc/ and that's because we moved one to the root.  Now if we try  /etc/passwd/., the result will be  /etc/passwd since dot refers to the current directory.
![[file_inclusion8.png]]

## Scenario-4
**the developer starts to use input validation by filtering some keywords. Let's test out and check the error message!**
```php
http://webapp.thm/index.php?lang=../../../../etc/passwd
```
We got the following error!
```php
Warning: include(languages/etc/passwd): failed to open stream: No such file or directory in /var/www/html/THM-5/index.php on line 15
```
If we check the warning message in the include(languages/etc/passwd) section, we know that the web application replaces the ../ with the empty string.

#### There are a couple of techniques we can use to bypass this.
1. First, we can send the following payload to bypass it: ....//....//....//....//....//etc/passwd

**Why did this work?**
This works because the PHP filter only matches and replaces the first subset string ../ it finds and doesn't do another pass, leaving what is pictured below.
![[file_inclusion9.png]]

![[file_inclusion10.png]]

## Scenario-5
**Finally, we'll discuss the case where the developer forces the include to read from a defined directory**
For example, if the web application asks to supply input that has to include a directory such as: http://webapp.thm/index.php?lang=languages/EN.php

#### Exploitation can be done as shown below:
then, to exploit this, we need to include the directory in the payload like so: ?lang=languages/../../../../../etc/passwd.
![[file_inclusion11.png]]
