## five main categories of vulnerabilities:
![[vulnerabilities1.png]]

## Scoring vulnerabilities
   - Vulnerability scoring serves a vital role in vulnerability management and is used to determine the potential risk and impact a vulnerability may have on a network or computer system.
   - For example, the popular Common Vulnerability Scoring System (CVSS) awards points to a vulnerability based upon its features, availability, and reproducibility.

### Common Vulnerability Scoring System(CVSS)
   - First introduced in 2005, the Common Vulnerability Scoring System (or CVSS) is a very popular framework for vulnerability scoring and has three major iterations.
   - As it stands, the current version is CVSSv3.1 (with version 4.0 currently in draft).
   
  
**A score is essentially determined by some of the following factors (but many more):**

1. How easy is it to exploit the vulnerability?

  2. Do exploits exist for this?

  3. How does this vulnerability interfere with the CIA triad?

##### Severity Rating Scale and their score ranges into the table below
![[vulnerabilities2.png]]

##### Let's analyse some of the advantages and disadvantages of CVSS in the table below:
![[vulnerabilities3.png]]

### Vulnerability Priority Rating (VPR)
   - The VPR framework is a much more modern framework in vulnerability management - developed by Tenable, an industry solutions provider for vulnerability management.
   - This framework is considered to be risk-driven; meaning that vulnerabilities are given a score with a heavy focus on the risk a vulnerability poses to the organisation itself, rather than factors such as impact (like with CVSS).

##### VPR uses a similar scoring range as CVSS, As shown below:
![[vulnerabilities4.png]]
   However, two notable differences are that VPR does not have a _"None/Informational"_ category, and because VPR uses a different scoring method, the same vulnerability will have a different score using VPR than when using CVSS.

##### Advantages and disadvantages of using the VPR framework in the table below:
![[vulnerabilities6.png]]

## Vulnerability databases
1. [NVD (National Vulnerability Database)](https://nvd.nist.gov/vuln/full-listing)

2. [Exploit-DB](http://exploit-db.com)

#### NVD – National Vulnerability Database
   - The National Vulnerability Database is a website that lists all publically categorised vulnerabilities.
   - In cybersecurity, vulnerabilities are classified under “**C**ommon **V**ulnerabilities and **E**xposures” (Or CVE for short).
   - These CVEs have the formatting of `CVE-YEAR-IDNUMBER`. For example, the vulnerability that the famous malware WannaCry used was `CVE-2017-0144.`
![[vulnerabilities7.png]]

#### Exploit-DB
   - Exploit-DB retains exploits for software and applications stored under the name, author and version of the software or application.
   - We can use Exploit-DB to look for snippets of code (known as Proof of Concepts) that are used to exploit a specific vulnerability.
![[vulnerabilities8.png]]
