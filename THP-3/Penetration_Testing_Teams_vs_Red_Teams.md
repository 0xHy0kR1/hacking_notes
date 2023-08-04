#### Penetration testing 
- Penetration Testing is the more rigorous and methodical testing of a network, application, hardware, etc.
- In short, you go through all the motions of Scoping, Intel Gathering, Vulnerability Analysis, Exploitation, Post Exploitation, and Reporting.
- In the traditional network test, we usually scan for vulnerabilities, find and take advantage of an exploitable system or application, maybe do a little post exploitation, find domain admin, and write up a report.
- For network pentests, we love getting to Domain Admin (DA) to gain access to the Domain Controller (DC).
- With penetration tests, we are lucky to get almost two weeks.
#### Red teams
- The Red Team’s mission is to emulate the tactics, techniques, and procedures (TTPs) by adversaries.
- The goals are to give real world and hard facts on how a company will respond, find gaps within a security program, identify skill gaps within employees, and ultimately increase their security posture.
- For Red Teams, it is not as methodical as penetration tests. Since we are simulating real world events, every test can differ significantly.
- For Red Team campaigns, based on the campaign, we may ignore the DC completely. One reason for this is that we are seeing many companies placing a lot of protection around their DCs.
- Another rule we follow is that we almost never run a vulnerability scan against the internal network because Vulnerability scans are very loud on the network and will most likely get caught.
- Whereas, Red Teams must build campaigns that last from 2 weeks to 6 months. This is because we need to simulate real attacks, social engineering, beaconing, and more.
- Red Team findings need to be geared more toward gaps in blue team processes, policies, tools, and skills.
- Two strong metrics that evolve from these campaigns are Time To Detect (TTD) and Time To Mitigate (TTM)
![[penetration_test_vs_red_teams.png]]

#### Penetration tests
1. Pre-engagement Interactions: Initial discussions and planning between parties before starting a project or collaboration.
    
2. Intelligence Gathering: Collecting information and data to understand the target or subject better.
    
3. Vulnerability Analysis: Identifying weaknesses or flaws in a system or process that could be exploited.
    
4. Exploitation: Actively taking advantage of the identified vulnerabilities to gain unauthorized access or control.
    
5. Post Exploitation: Activities carried out after successful exploitation to maintain access or gather additional information.
    
6. Reporting: Presenting findings and results from the engagement, including vulnerabilities discovered and potential remediation steps.

#### Red Teams
1. Intelligence Gathering: Collecting information and data about the target system or organization.
    
2. Initial Foothold: Gaining the first point of entry into the target system or network.
    
3. Persistence/Local Privilege: Establishing ways to maintain access and obtaining local user privileges.
    
4. Escalation: Elevating privileges to gain higher levels of access and control.
    
5. Local/Network Enumeration: Scanning and discovering resources and services available on the local system or network.
    
6. Lateral Movement: Moving laterally within the network to explore and compromise other connected systems.
    
7. Data Identification/Exfiltration: Locating and extracting valuable or sensitive data from the compromised systems.
    
8. Domain Privilege Escalation/Dumping Hashes: Elevating privileges to gain control over the entire network domain or stealing password hashes for further attacks.
    
9. Reporting: Documenting and communicating the results and findings of the engagement.

## Some resources to learn red teamers assements
**Fire-eye report** --> [[fire-eye_twitter_report.pdf]]

- A detailed breakdown for APT attacks is MITRE’s Adversarial Tactics, Techniques, and Common Knowledge (ATT&CK) matrix. This is a large collection of different TTPs commonly used with all sorts of attacks.

- Another resource is this running list of APT Groups and Operations document from @cyb3rops.
https://docs.google.com/spreadsheets/d/1H9_xaxQHpWaa4O_Son4Gx0YOIzlcBWMsdvePFX68EKU/edit#gid=361554658
- This completely breaks down different suspected APT groups and their toolsets. This is a useful list for us as Red Teamers to simulate different attacks.

- The team at Red Canary supplied detailed information on each one of these techniques(red team techniques). I highly recommend you take time and review them all: http://bit.ly/2H0MTZA