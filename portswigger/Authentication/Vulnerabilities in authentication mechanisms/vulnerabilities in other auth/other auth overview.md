- In addition to the basic login functionality, most websites provide supplementary functionality to allow users to manage their account. For example, users can typically change their password or reset their password when they forget it. These mechanisms can also introduce vulnerabilities that can be exploited by an attacker.
- This is especially important in cases where an attacker is able to create their own account and, consequently, has easy access to study these additional pages.

## Keeping users logged in
- A common feature is the option to stay logged in even after closing a browser session. This is usually a simple checkbox labeled something like "Remember me" or "Keep me logged in".
- This functionality is often implemented by generating a "remember me" token of some kind, which is then stored in a persistent cookie.
- However, some websites generate this cookie based on a predictable concatenation of static values, such as the username and a timestamp. Some even use the password as part of the cookie. This approach is particularly dangerous if an attacker is able to create their own account because they can study their own cookie and potentially deduce how it is generated. Once they work out the formula, they can try to brute-force other users' cookies to gain access to their accounts.
- Some websites assume that if the cookie is encrypted in some way it will not be guessable even if it does use static values.
- the cookie using a simple two-way encoding like Base64 offers no protection whatsoever. Even using proper encryption with a one-way hash function is not completely bulletproof. If the attacker is able to easily identify the hashing algorithm, and no salt is used, they can potentially brute-force the cookie by simply hashing their wordlists.
- This method can be used to bypass login attempt limits if a similar limit isn't applied to cookie guesses.
