- Now, in normal client-server communication, there are a series of requests followed by responses. The idea behind an SMB Relay attack is to position yourself between the client and the server in order to capture the data packets transmitted between the two entities.
1. Introduction to SMB relay attack:
   ![[AD_in_SMB_relay1.png]]

2. modifying Responder.conf file to not respond to any of SMB stuffs but listen for SMB and HTTP. It means that, we are listening for hashes and relay this hashes with other tool.
   ![[AD_in_SMB_relay2.png]]

3. Responder configuration file after modification. 
   ![[AD_in_SMB_relay3.png]]

4. With "ntlmrelayx.py" we just those hashes to targets(specified with targets.txt) and there is a `-smb2support` switch to incorporate with smb2.
   ![[AD_in_SMB_relay4.png]]
5. machine try to use DNS to identify this machine that passes hashes to this windows machine but fails and event occur. 
   ![[AD_in_SMB_relay5.png]]

6. We get the hashes of local users(not the domain users) that we want it.
   ![[AD_in_SMB_relay6.png]]

