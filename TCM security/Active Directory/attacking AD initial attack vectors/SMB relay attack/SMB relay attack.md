1. modifying Responder.conf file to not respond to any of SMB stuffs but listen for SMB and HTTP. It means that, we are listening for hashes and relay this hashes to other tool.
   ![[AD_in_SMB_relay2.png]]

2. Responder configuration file after modification. 
   ![[AD_in_SMB_relay3.png]]
- We need to turn off SMB and HTTP servers as we do not want to respond to these protocols as we will be capturing the hash and relaying it to a different tool called `ntlmrelayx.py`
- Responder has caught the user 'frank castle attempting to browse to a host that does not exists on the network. After DNS has failed to resolve the machine falls back to LLMNR which in this case we have caught the hash and relayed it over to ntlmrelayx.py.

3. With "ntlmrelayx.py" we just pass those hashes to targets(specified with targets.txt) and there is a `-smb2support` switch to incorporate with smb2.
   ![[AD_in_SMB_relay4.png]]
   ntlmrelayx.py then forwards the hash over to the machines specified with the `-tf` switch which in this case is 192.168.1.18 or frank castle.
   
4. machine try to use DNS to identify this machine that passes hashes to this windows machine but fails and event occur. 
   ![[AD_in_SMB_relay5.png]]

6. We get the hashes of local users(not the domain users) that we want it.
   ![[AD_in_SMB_relay6.png]]
   As the user 'frank castle' is an administrator on windows enterprise 2, `ntlmrelayx.py` has allowed us to dump the hashes in the SAM database.