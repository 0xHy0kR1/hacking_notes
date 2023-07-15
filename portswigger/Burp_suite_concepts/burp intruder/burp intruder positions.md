## What is intruder?
It allows us to take a request (usually captured in the Proxy before being passed into Intruder) and use it as a template to send many more requests with slightly altered values automatically.

**we sent a request in from the Proxy (by using `Ctrl + I` or right-clicking and selecting "Send to Intruder")**

## There are four other Intruder sub-tabs:
1. **Positions:**
	- allows us to select an Attack Type.
2. **Payloads:**
	- allows us to select values to insert into each of the positions we defined in the previous sub-tab.
	- In simple terms, It tells Intruder where to insert payloads
	- **Example**: we may choose to load items in from a wordlist to serve as payloads.
3. **Resource Pool**:
	- It allows us to divide our resources between tasks.
	- Burp Pro would allow us to run various types of automated tasks in the background, which is where we may wish to manually allocate our available memory and processing power between these automated tasks and Intruder.
4. **Options**:
	- The settings here apply primarily to how Burp handles results.
![[burp_basics1.png]]

## Right panel overview of intruder:
- **Add** lets us define new positions by highlighting them in the editor and clicking the button.
- **Clear** removes all defined positions, leaving us with a blank canvas to define our own.
- **Auto** attempts to select the most likely positions automatically; this is useful if we cleared the default positions and want them back.

