## What is an SSRF?
- SSRF stands for Server-Side Request Forgery.
- It's a vulnerability that allows a malicious user to cause the webserver to make an additional or edited HTTP request to the resource of the attacker's choosing.

## Types of SSRF
- the first is a regular SSRF where data is returned to the attacker's screen.
- The second is a Blind SSRF vulnerability where an SSRF occurs, but no information is returned to the attacker's screen.

## What's the impact?
- Access to unauthorised areas.
- Access to customer/organisational data.
- Ability to Scale to internal networks.
- Reveal authentication tokens/credentials.

## SSRF example
![[SSRF1.png]]

1. Scenario-1 --> directory traversal:
![[SSRF2.png]]
- It demonstrates how an attacker can still get to the /api/user page even if they only have control over the path by using **directory traversal**.
- When website.thm receives (**../**), it is a message to **move up a directory**, which removes the /stock component of the request and **converts the final request to /api/user**.

2. Scenario-2 --> attack has to subdomain of server:
![[SSRF3.png]]
- The attacker has access to the server’s subdomain to which the request is directed.
- Take note of the payload ending in **&x=**, which is used to prevent the remaining path from being connected to the end of the attacker’s URL and instead turns it into a query string parameter (**?x=**).

3. Scenario-3 --> server request to attack domain:
![[SSRF4.png]]
- Returning to the original request, the attacker can cause the webserver to request a server of his or her preference.
- We can capture request headers submitted to the attacker’s designated domain by doing so. These headers may include authentication credentials or API keys delivered by the website.thm (that would normally authenticate to api.website.thm).

## four common places to look for SSRF vulns:
![[SSRF5.png]]

## Approaches to mitigate SSRF vuln:
1. Deny list:
	- A Deny List is where all requests are accepted apart from resources specified in a list or matching a particular pattern.
	- A Web Application may employ a deny list to protect sensitive endpoints, IP addresses or domains from being accessed by the public while still allowing access to other locations.
	- 127.0.0.1 would appear on a deny list.
	- Attackers can bypass a Deny List by using alternative localhost references such as 0, 0.0.0.0, 0000, 127.1, 127.*.*.*, 2130706433, 017700000001 or subdomains that have a DNS record which resolves to the IP Address 127.0.0.1 such as 127.0.0.1.nip.io.
	- Also, in a cloud environment, it would be beneficial to block access to the IP address 169.254.169.254, which contains metadata for the deployed cloud server, including possibly sensitive information.
	- An attacker can bypass this by registering a subdomain on their own domain with a DNS record that points to the IP Address 169.254.169.254.

2. Allow List:
	- An allow list is where all requests get denied unless they appear on a list or match a particular pattern, such as a rule that an URL used in a parameter must begin with **https://website.thm.**
	- An attacker could quickly circumvent this rule by creating a subdomain on an attacker's domain name, such as https://website.thm.attackers-domain.thm. The application logic would now allow this input and let an attacker control the internal HTTP request.
	**Open Redirect**
	- If the above bypasses do not work, there is one more trick up the attacker's sleeve, the open redirect.
	- An open redirect is an endpoint on the server where the website visitor gets automatically redirected to another website address.
	- ake, for example, the link https://website.thm/link?url=https://tryhackme.com. This endpoint was created to record the number of times visitors have clicked on this link for advertising/marketing purposes.
	- But imagine there was a potential SSRF vulnerability with stringent rules which only allowed URLs beginning with https://website.thm/. An attacker could utilise the above feature to redirect the internal HTTP request to a domain of the attacker's choice.

