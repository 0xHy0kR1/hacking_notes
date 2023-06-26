## We are going to solve this exercise using batch script:
1. posting random data to test that we get reply back from server or not:
```python
┌──(hyok㉿kali)-[~/burp_scripts]
└─$ curl -X POST -d "username=test&password=test" https://0ab000a60489ac2f84e514a4003e003a.web-security-academy.net/login
```

2. Displaying the size of the page:
   
```python
┌──(hyok㉿kali)-[~/burp_scripts]
└─$ curl -X POST -d "username=test&password=test" -so /dev/null https://0ab000a60489ac2f84e514a4003e003a.web-security-academy.net/login -w '%{size_download}'
3132 
```
-so --> `-s` is for silent mode, so that we won't see any other progress bar and `o` is for any other contents of request gets redirected.

-d --> for data

-w --> getting the size of response page

3. Checking that if any of the username is lock out
![[username_enumeration via_account_lock4.png]]

4. Now, we output the result to a file:
   You can redirect the output by just putting `> file_name.txt` at the end of command to redirect the output.

5. Now, extracting the valid user from valid_user.txt file, as shown below;
![[username_enumeration via_account_lock5.png]]
**Result** - Valid user is "aq".

6. Now, brute-forcing to get the password "aq" user:
![[username_enumeration_via_different_responses6.png]]

7. Now, extracting the valid user of correct pasword from valid_user.txt file, as shown below;
