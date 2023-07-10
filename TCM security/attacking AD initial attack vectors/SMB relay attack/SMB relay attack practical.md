# Pre-requisite --> [[LLMNR poisoning]]

## Scenario -->
We will be capturing a hash on fcastle using LLMNR Poisoning and performing a SMB relay attack to gain SAM database hashes on peter parker.

**Note** - 
1. fcastle should be logged in peter parker before the start of attack.
## Steps to perform SMB relay attack:
1. modifying Responder.conf file to not respond to any of SMB stuffs but listen for SMB and HTTP. It means that, we are listening for hashes and relay this hashes to other tool.
   ![[AD_in_SMB_relay2.png]]

2. Responder configuration file after modification. 
![[AD_in_SMB_relay3.png]]
- We need to turn off SMB and HTTP servers as we do not want to respond to these protocols as we will be capturing the hash and relaying it to a different tool called `ntlmrelayx.py`
- Responder has caught the user 'frank castle attempting to browse to a host that does not exists on the network. After DNS has failed to resolve the machine falls back to LLMNR which in this case we have caught the hash and relayed it over to ntlmrelayx.py.

3. With "ntlmrelayx.py" we just pass those hashes to targets(specified with targets.txt) and there is a `-smb2support` switch to incorporate with smb2.
![[SMB_relay_attack4.png]]
Note --> hash come from 192.168.1.16 through responder and goes to 192.168.1.18 and the event triggered by 192.168.1.16.

