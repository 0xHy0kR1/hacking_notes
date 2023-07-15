## There are four attack types available:
- Sniper
- Battering ram
- Pitchfork
- Cluster bomb

1. Sniper:
	- When conducting a sniper attack, we provide _one_ set of payloads.
	- **Example** - this could be a single file containing a wordlist or a range of numbers.
![[burp_basics2.png]]
There are two positions defined here, targeting the `username` and `password` body parameters.

**Example-2** - 
For example, let's assume we have a wordlist with three words in it: `burp`, `suite`, and `intruder`. Intruder would use these words to make **_six_** requests:
![[burp_basics3.png]]

2. **Battering Ram:**
	- the Battering ram puts the same payload in _every_ position rather than in each position in turn.
	- **Example** - 
![[burp_basics4.png]]
If we use Battering ram to attack this, Intruder will take each payload and substitute it into every position _at once._

**Example-2** - 
For example, let's assume we have a wordlist with three words in it: `burp`, `suite`, and `intruder`. Intruder would make _three_ requests:
![[burp_basics5.png]]

3. **Pitchfork**:
	- Pitchfork as being like having numerous Snipers running simultaneously.
	- Where Sniper uses _one_ payload set (which it uses on every position simultaneously), Pitchfork uses one payload set per position (up to a maximum of 20) and iterates through them all at once.
**Example-1** - 
- Our first wordlist will be usernames. It contains three entries: `joel`, `harriet`, `alex`.
- Let's say that Joel, Harriet, and Alex have had their passwords leaked: we know that Joel's password is `J03l`, Harriet's password is `Emma1815`, and Alex's password is `Sk1ll`.  
    
We can use these two lists to perform a pitchfork attack on the login form from before.

**When using Intruder in pitchfork mode, the requests made would look something like this:**
![[burp_basics6.png]]

**Note** - if we have two lists, one with 100 lines and one with 90 lines, Intruder will only make 90 requests, and the final ten items in the first list will not get tested.

4. **Cluster Bomb**:
	- Like Pitchfork, Cluster bomb allows us to choose multiple payload sets: one per position, up to a maximum of 20.
	- however, whilst Pitchfork iterates through each payload set simultaneously, Cluster bomb iterates through each payload set individually, making sure that every possible combination of payloads is tested.
**Example-1** - 
use the same wordlists as before:
- Usernames: `joel`, `harriet`, `alex`.
- Passwords: `J03l`, `Emma1815`, `Sk1ll`.

**The request table for our username and password positions looks something like this:**
![[burp_basics7.png]]

