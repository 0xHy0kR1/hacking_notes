- Consider an application that lets users log in with a username and password. If a user submits the username `wiener` and the password `bluecheese`.
- the application checks the credentials by performing the following SQL query:
```sql
`SELECT * FROM users WHERE username = 'wiener' AND password = 'bluecheese'`
```

- If the query returns the details of a user, then the login is successful. Otherwise, it is rejected.
- For example, submitting the username `administrator'--` and a blank password results in the following query:
```sql
`SELECT * FROM users WHERE username = 'administrator'--' AND password = ''`
```
- This query returns the user whose username is `administrator` and successfully logs the attacker in as that user.

## LAB solution
![[without_username_access.png]]