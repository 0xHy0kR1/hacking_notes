## What is username enumeration?
- Username enumeration is a technique used by attackers to identify valid usernames or user accounts within a system or application.
- The process of username enumeration typically involves making repeated login attempts using different usernames and observing the system's response. By analyzing the system's behavior, an attacker can determine whether a particular username exists in the system or not.
- Username enumeration typically occurs either on the login page, for example, when you enter a valid username but an incorrect password, or on registration forms when you enter a username that is already taken.

**While attempting to brute-force a login page, you should pay particular attention to any differences in:**
1. Status codes:
	- During a brute-force attack, the returned HTTP status code is likely to be the same for the vast majority of guesses because most of them will be wrong. If a guess returns a different status code, this is a strong indication that the username was correct.

2. Error messages:
	- Sometimes the returned error message is different depending on whether both the username AND password are incorrect or only the password was incorrect.

3. Response times:
	- A website might only check whether the password is correct if the username is valid. This extra step might cause a slight increase in the response time, This may be subtle, but an attacker can make this delay more obvious by entering an excessively long password

