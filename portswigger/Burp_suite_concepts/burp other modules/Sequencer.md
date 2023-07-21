## Introduction 
- Sequencer allows us to measure the entropy of "tokens" -- strings that are used to identify something and should, in theory, be generated in a cryptographically secure manner.
**Example** - 
we may wish to analyse the randomness of a session cookie or a **C**ross-**S**ite **R**equest **F**orgery (CSRF) token.
![[burp_basics26.png]]

**There are two main methods we can use to perform token analysis with Sequencer:**
1. **Live capture**
	- It is the more common of the two methods.
	- Live capture allows us to pass a request to Sequencer, which we know will create a token for us to analyse.
**Example** - 
we may wish to pass a POST request to a login endpoint into Sequencer, as we know that the server will respond by giving us a cookie. With the request passed in, we can tell Sequencer to start a live capture: it will then make the same request thousands of times automatically, storing the generated token samples for analysis. Once we have accumulated enough samples, we stop Sequencer and allow it to analyse the captured tokens.

2. **Manual load**
	- It allows us to load a list of pre-generated token samples straight into Sequencer for analysis.
	- Using Manual Load means we don't have to make thousands of requests to our target, but it does mean that we need to obtain a large list of pre-generated tokens!

## Practical 
1. We will start by capturing a request to `http://10.10.23.208/admin/login/` in the Proxy. Right-click on the request and choose "Send to Sequencer":
![[burp_basics27.png]]
In this instance, we are testing the `loginToken`, so select the radio button for "Form field":

2. A new window will now pop up telling us that we are performing a live capture and showing us how many tokens we have so far captured.
3. Once you have around 10,000 tokens captured, click "Pause", then select the "Analyze now" button:
![[burp_basics28.png]]
If we wanted to receive periodic updates on the analysis, we could also have checked the "Auto analyze" checkbox.
4. Having clicked the "Analyze now" button, Burp will proceed to analyse the entropy of our token and generate a report.

