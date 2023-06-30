## Introduction
- An IDOR, which stands for Insecure Direct Object Reference, refers to a vulnerability that can occur in web applications where user-accessible objects are referenced directly without proper authorization checks.
- In simpler terms, it means that an attacker can manipulate the application's parameters or object references to access unauthorized resources or perform actions that they shouldn't be able to.
**Example** - 
A web application that allows users to view their personal information by accessing URLs like "[https://example.com/user/profile?user_id=123](https://example.com/user/profile?user_id=123)".
In this case, the user ID is used as a parameter to retrieve the user's profile from the server and display it on the page.
The vulnerability arises when the application fails to validate the user's authorization properly.If the application does not enforce proper access controls, an attacker could modify the "user_id" parameter in the URL to access the profile of another user, such as "[https://example.com/user/profile?user_id=456](https://example.com/user/profile?user_id=456)"By simply changing the value of the "user_id" parameter.

## Encoded IDs
![[encoded_ids.png]]

## Hashed IDs 
- For example, the Id number 123 would become 202cb962ac59075b964b07152d234b70 if md5 hashing were in use.
- Check [https://crackstation.net/](https://crackstation.net/) to crack any hash.

## Unpredictable IDs
If the Id cannot be detected using the above methods, an excellent method of IDOR detection is to create two accounts and swap the Id numbers between them. If you can view the other users' content using their Id number while still being logged in with a different account (or not logged in at all), you've found a valid IDOR vulnerability.
