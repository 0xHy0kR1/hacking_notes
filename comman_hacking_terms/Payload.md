- This is the actual code which does the work. It runs on the system after exploitation.
- It is mostly used to set up a connection between the attacking and victim machines.
- Metasploit has more than 500 payloads.
## There are three different types of payload module in the Metasploit Framework:
### Single
- Singles are payloads that are self-contained and completely standalone.
- A single payload can be something as simple as adding a user to the target system or running an executable.

## Stager
- A stager will set up a network connection between the attacker and victim, and it is designed to be small and reliable.

## Stages
- Stages are payload components downloaded by the stager, and provide advanced features with no size limits such as `dllinject, meterpreter, patchupdllinject, upexec, vncinject,` among others.