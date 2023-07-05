## What is stored XSS?
As the name infers, the XSS payload is stored on the web application (in a database, for example) and then gets run when other users visit the site or web page.

## Example Scenario:
A blog website that allows users to post comments. Unfortunately, these comments aren't checked for whether they contain JavaScript or filter out any malicious code.
If we now post a comment containing JavaScript, this will be stored in the database, and every other user now visiting the article will have the JavaScript run in their browser.
![[XSS4.png]]

## Potential Impact:
The malicious JavaScript could redirect users to another site, steal the user's session cookie, or perform other website actions.

**How to test for Stored XSS**:
You'll need to test every possible point of entry where it seems data is stored and then shown back in areas that other users have access to;
**Example**
- Comments on a blog
- User profile information  
- Website Listings