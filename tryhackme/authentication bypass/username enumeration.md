  

If you try entering the username **admin** and fill in the other form fields with fake information, you'll see we get the error **An account with this username already exists**.
  
If you try entering the username **admin** and fill in the other form fields with fake information, you'll see we get the error **An account with this username already exists**.
```python
user@tryhackme$ ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.66.70/customers/signup -mr "username already exists"
```
	- `-w` argument selects the file's location that contains the list of usernames
	- `-X` argument specifies the request method this will be a GET request by default, but it is a POST request above.
	- `-d` argument specifies the data that we are going to send.
	- `-H` argument is used for adding additional headers to the request. In this instance, we're setting the `Content-Type` to the webserver knows we are sending form data.
	- `-u` argument specifies the URL we are making the request to.
	- `-mr` argument is the text on the page we are looking for to validate we've found a valid username.
	