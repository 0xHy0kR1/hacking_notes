## Introduction
- They are not vulnerabilities regarding bad implementations or configurations, but the idea behind the whole application (or a part of it) is flawed from the start.
- Some other times, insecure design vulnerabilities may also be introduced by developers while adding some "shortcuts" around the code to make their testing easier.

**Example** - 
A developer could disable the OTP validation in the development phases to quickly test the rest of the app without manually inputting a code at each login but forget to re-enable it when sending the application to production.

## Insecure Password Resets
**Example** - 
Instagram allowed users to reset their forgotten passwords by sending them a 6-digit code to their mobile number via SMS for validation.
If an attacker wanted to access a victim's account, he could try to brute-force the 6-digit code. As expected, this was not directly possible as Instagram had rate-limiting implemented so that after 250 attempts, the user would be blocked from trying further.
![[insecure_design1.png]]
However, it was found that the rate-limiting only applied to code attempts made from the same IP. so an attacker would need 1000000/250 = 4000 IPs to cover all possible codes.
