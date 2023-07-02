- which help you to define the rules and scope for each session Burp carries out.

## Each rule has two parts:
- A **scope** denoting the tools, URLs and parameters that the rule applies to.
- The **actions** that are performed when the rule is applied to a request.

**For example, you could define the following rules for a particular test:**
- For all requests, add cookies from Burp's cookie jar.
- For requests to a specific domain, validate that the current session with that application is still active. If the session is not active, run a macro to log back in to the application, and update the cookie jar with the resulting session token.
- For requests to a specific URL containing the `__csrftoken` parameter, run a macro to obtain a valid `__csrftoken` value and use this value when making the request.