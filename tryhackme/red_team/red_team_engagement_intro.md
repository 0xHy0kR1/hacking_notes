#### Red team engagements come in many varieties; including,
- Tabletop exercises 
- Adversary emulation
- Physical assessment

## Defining Scope and Objectives

##### Client objectives
   - Client objectives should be discussed between the client and red team to create a mutual understanding between both parties of what is expected and provided.
   - Set objectives are the basis for the rest of the engagement documentation and planning.

**Example - Global Enterprises:**

**Objectives:**

1. Identify system misconfigurations and network weaknesses.
    1. Focus on exterior systems.
2. Determine the effectiveness of endpoint detection and response systems.
3. Evaluate overall security posture and response.
    1. SIEM and detection measures.
    2. Remediation.
    3. Segmentation of DMZ and internal servers.
4. Use of white cards is permitted depending on downtime and length.
5. Evaluate the impact of data exposure and exfiltration.
##### Client scope
   - A client's scope will typically define what you cannot do or target; it can also include what you can do or target. a scope should only be set by the client.

**Scope:**

1. System downtime is not permitted under any circumstances.
    1. Any form of DDoS or DoS is prohibited.
    2. Use of any harmful malware is prohibited; this includes ransomware and other variations.
2. Exfiltration of PII is prohibited. Use arbitrary exfiltration data.
3. Attacks against systems within 10.0.4.0/22 are permitted.
4. Attacks against systems within 10.0.12.0/22 are prohibited.
5. Bean Enterprises will closely monitor interactions with the DMZ and critical/production systems.
    1. Any interaction with "*.bethechange.xyz" is prohibited.
    2. All interaction with "*.globalenterprises.thm" is permitted.


**below is an example a client's scope**
- No exfiltration of data.
- Production servers are off-limits.
- 10.0.3.8/18 is out of scope.
- 10.0.0.8/20 is in scope.
- System downtime is not permitted under any circumstances.
- Exfiltration of PII is prohibited.

