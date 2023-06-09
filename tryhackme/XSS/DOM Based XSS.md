## What is the DOM?
- DOM stands for **D**ocument **O**bject **M**odel and is a programming interface for HTML and XML documents.
- A diagram of the HTML DOM is displayed below:
![[XSS5.png]]

## Exploiting the DOM
- DOM Based XSS is where the JavaScript execution happens directly in the browser without any new pages being loaded or data submitted to backend code.
- Execution occurs when the website JavaScript code acts on input or user interaction.

## Example Scenario:
The website's JavaScript gets the contents from the `window.location.hash` parameter and then writes that onto the page in the currently being viewed section.
The contents of the hash aren't checked for malicious code, allowing an attacker to inject JavaScript of their choosing onto the webpage.

## Potential Impact:
Crafted links could be sent to potential victims, redirecting them to another website or steal content from the page or the user's session.

## How to test for Dom Based XSS:
- DOM Based XSS can be challenging to test for and requires a certain amount of knowledge of JavaScript to read the source code.
- You'd need to look for parts of the code that access certain variables that an attacker can have control over, such as "**window.location.x**" parameters.

## What unsafe JavaScript method is good to look for in source code?
eval()