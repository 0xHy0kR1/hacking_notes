## What is Replected XSS?
Reflected XSS happens when user-supplied data in an HTTP request is included in the webpage source without any validation.

## Example Scenario:
  
A website where if you enter incorrect input, an error message is displayed. The content of the error message gets taken from the **error** parameter in the query string and is built directly into the page source.
![[XSS1.png]]

The application doesn't check the contents of the **error** parameter, which allows the attacker to insert malicious code.
![[XSS2.png]]

The vulnerability can be used as per the scenario in the image below:
![[XSS3.png]]

## Potential Impact:
The attacker could send links or embed them into an iframe on another website containing a JavaScript payload to potential victims getting them to execute code on their browser, potentially revealing session or customer information.

## How to test for Reflected XSS:
You'll need to test every possible point of entry; these include:
- Parameters in the URL Query String
- URL File Path
- Sometimes HTTP Headers (although unlikely exploitable in practice)

