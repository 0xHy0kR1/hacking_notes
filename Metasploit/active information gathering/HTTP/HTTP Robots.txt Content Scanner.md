- The `auxiliary/scanner/http/robots_txt` module in Metasploit is used to check if a web server has a file called "robots.txt".
- robots.txt file is used to tell web crawlers, like those used by search engines, which pages they can and can't access on a website.
- By scanning for the presence of a robots.txt file, this module can give you information about how the website is configured and what pages or directories are intended to be hidden from search engines. This information can be useful in discovering potential vulnerabilities on the website.
# Code -
```python
msf6 auxiliary(scanner/http/cert) > use auxiliary/scanner/http/robots_txt
msf6 auxiliary(scanner/http/robots_txt) > set RHOSTS 188.184.21.108
RHOSTS => 188.184.21.108
msf6 auxiliary(scanner/http/robots_txt) > run

[*] [188.184.21.108] /robots.txt found
[+] Contents of Robots.txt:
#
# Robots.txt file for all AFS and EOS Web servers
#
# Same file for all servers

User-agent: *
Allow: /authoring/
Allow: /cnellist/
Allow: /cms-tracker/
Allow: /club-badminton-bst2016/
Allow: /CLICr/
Allow: /davidc/
Allow: /droussea/
Allow: /dd4hep/
Allow: /edreyer/
Allow: /edreyer
Allow: /flair
Allow: /gfasanel/
Allow: /geant4/
Allow: /grid-deployment/
Allow: /glite/
Allow: /gsalam/
Allow: /hrussell/
Allow: /ibarrien/
Allow: /lhcbqa/
Allow: /lhcbproject/Publications/
Allow: /luxqed/
Allow: /mad/
Allow: /mdudek/
Allow: /mig/
Allow: /mcfayden/
Allow: /pmarino/
Allow: /pvankov/
Allow: /project-allpix-squared/
Allow: /radnext-network/
Allow: /rtomas/
Allow: /swedish/
Allow: /spectrum/
Allow: /shoh/
Allow: /srettie/
Allow: /siodmok/
Allow: /stapley/
Allow: /sviel/
Allow: /theofil/
Allow: /track-it-documentation/
Allow: /tvami/
Allow: /hedberg/
Disallow: /yachting/BBoard
Allow: /yachting/
Disallow: /


User-agent: FAST Enterprise Crawler 6 used by CERN (project-search@cern.ch)
Disallow:
Disallow: /proj-fgc/

User-agent: FAST Enterprise Crawler for Sharepoint used by CERN (project-search@cern.ch)
Disallow:
Disallow: /proj-fgc/

User-agent: CERN Search Crawler
Allow: /
Disallow:
Disallow: /proj-fgc/


[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```