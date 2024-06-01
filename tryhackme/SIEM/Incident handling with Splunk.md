**Below are a few of the events that would negatively affect the environment when they occurred:**
- Crashing the system
- Execution of an unwanted program
- Access to sensitive information from an unauthorized user
- A Website being defaced by the attacker
- The use of USB devices when there is a restriction in usage is against the company's policy

## Incident Handling Life Cycle
![[incident_handling_life_cycle.png]]

   - As an Incident Handler / SOC Analyst, we would aim to know the attackers' tactics, techniques, and procedures. Then we can stop/defend/prevent against the attack in a better way.

**The Incident Handling process is divided into four different phases.**

#### 1. Preparation
   - The preparation phase covers the readiness of an organization against an attack. That means documenting the requirements, defining the policies, incorporating the security controls to monitor like EDR / SIEM / IDS / IPS, etc.
   - It also includes hiring/training the staff.

#### 2. Detection and Analysis
   - The detection phase covers everything related to detecting an incident and the analysis process of the incident.
   - This phase covers getting alerts from the security controls like SIEM/EDR investigating the alert to find the root cause.
   - This phase also covers hunting for the unknown threat within the organization.

##### 3. Containment, Eradication, and Recovery
   - This phase covers the actions needed to prevent the incident from spreading and securing the network.
   - It involves steps taken to avoid an attack from spreading into the network, isolating the infected host, clearing the network from the infection traces, and gaining control back from the attack.

##### 4. Post-Incident Activity / Lessons Learnt
  - This phase includes identifying the loopholes in the organization's security posture, which led to an intrusion, and improving so that the attack does not happen next time.
  - The steps involve identifying weaknesses that led to the attack, adding detection rules so that similar breach does not happen again, and most importantly, training the staff if required.

## Incident Handling: Scenario
**Cyber Kill Chain phases** - 
![[splunk12.png]]
   - We will follow the Cyber kill Chain Model and map the attacker's activity in each phase during this Investigation.
   - When required, we will also utilize Open Source Intelligence (OSINT) and other findings to fill the gaps in the kill chain.

**It is not necessary to follow this sequence of the phases while investigating.**
- Reconnaissance
- Weaponization
- Delivery
- Exploitation
- Installation
- Command & Control
- Actions on Objectives

#### Scenario
   - A Big corporate organization **Wayne Enterprises** has recently faced a cyber-attack where the attackers broke into their network, found their way to their web server, and have successfully defaced their website **http://www.imreallynotbatman.com**.
   - Their website is now showing the trademark of the attackers with the message **YOUR SITE HAS BEEN DEFACED** as shown below.
![[splunk13.png]]

We have got all the event logs related to the attacker's activities with the help splunk. We need to explore the records and find how the attack got into their network and what actions they performed.  

This Investigation comes under the `Detection and Analysis phase.`

**Splunk**
   - During our investigation, we will be using `Splunk` as our SIEM solution.

To get the complete picture of the hosts and log sources being monitored in Wayne Enterprise, please click on the **Data summary** and navigate the available tabs to get the information.
![[analyze_attack.gif]]

**Interesting log Sources**
   Some of the interesting log sources that will help us in our Investigation are:
![[splunk14.png]]

**Note:** All the event logs that we are going to investigate are present in `index=botsv1`

### Reconnaissance Phase
   Reconnaissance is an attempt to discover and collect information about a target. It could be knowledge about the system in use, the web application, employees or location, etc.

Let's start by searching for the domain in the search head and see which log source includes the traces of our domain.

**Search Query**: `index=botsv1 imreallynotbatman.com`

**Search Query explanation:** We are going to look for the event logs in the index "botsv1" which contains the term `imreallynotbatman.com`

![[scenario_log_check.gif]]
   - In the sourcetype field, we saw that the following log sources contain the traces of this search term.
	- Suricata
	- stream:http - It contains the http traffic logs.
	- fortigate_utm
	- iis

**Note** - Our first task is to identify the IP address attempting to perform reconnaissance activity on our web server.

**Search Query:** `index=botsv1 imreallynotbatman.com sourcetype=stream:http`

**Search Query Explanation:** This query will only look for the term  `imreallynotbatman.com`in the **stream:http** log source.
![[splunk15.png]]

**Note:**
   The important thing to note, if you don't find the field of interest, keep scrolling in the left panel. When you click on a field, it will contain all the values it finds in the logs.

**To further confirm our suspicion about the IP address "40.80.148.42", click on the IP and examine the logs. We can look at the interesting fields like User-Agent, Post request, URIs, etc., to see what kind of traffic is coming from this particular IP.**
![[scenario_log_check.gif]]
   - We have narrowed down the results to only show the logs from the source IP **40.80.148.42**, looked at the fields of interest and found the traces of the domain being probed.

### Validate the IP that is scanning
   So what do we need to do to validate the scanning attempt? Simple, dig further into the weblogs. Let us narrow down the result, look into the `suricata` logs, and see if any rule is triggered on this communication.

**Search Query:** `index=botsv1 imreallynotbatman.com src=40.80.148.42 sourcetype=suricata`

**Search Query Explanation:** This query will show the logs from the suricata log source that are detected/generated from the source IP **40.80.148.42**

![[scenario_sunricata_log_check.gif]]
   - We have narrowed our search on the **src IP** and looked at the source type `suricata` to see what Suricata triggered alerts.
   - In the right panel, we could not find the field of our interest, so we clicked on more fields and searched for the fields that contained the signature alerts information, which is an important point to note.

#### Questions
1. One suricata alert highlighted the CVE value associated with the attack attempt. What is the CVE value?
Ans - CVE-2014-6271
![[splunk16.png]]

2. What is the CMS our web server is using?
Ans - Joomla
![[splunk17.png]]

3. What is the web scanner, the attacker used to perform the scanning attempts?
Ans - Acunetix
![[splunk18.png]]

4. What is the IP address of the server imreallynotbatman.com?
Ans -  192.168.250.70

## Exploitation Phase

**To begin our investigation, let's note the information we have so far:**
- We found two IP addresses from the reconnaissance phase with sending requests to our server.
- One of the IPs `40.80.148.42` was seen attempting to scan the server with IP **192.168.250.70**.
- The attacker was using the web scanner Acunetix for the scanning attempt.

### Count

**Let's use the following search query to see the number of counts by each source IP against the webserver.**

**Search Query**:`index=botsv1 imreallynotbatman.com sourcetype=stream* | stats count(src_ip) as Requests by src_ip | sort - Requests`

**Query Explanation:**   
This query shows how many times each IP address appears in the "src_ip" field using the stats function.
![[splunk19.png]]

**Additionally, we can also create different visualization to show the result. Click on "Visualization → Select Visualization" as shown below.**
![[splunk20.png]]
Now we will narrow down the result to show requests sent to our web server, which has the IP `192.168.250.70`

**Search Query:** `index=botsv1 sourcetype=stream:http dest_ip="192.168.250.70"`
**Query Explanation:** This query will look for all the inbound traffic towards IP **192.168.250.70.**
![[splunk21.png]]
   - The result in the **src_ip** field shows three IP addresses (1 local IP and two remote IPs) that originated the HTTP traffic towards our webserver.
   - Another interesting field, **http_method** will give us information about the HTTP Methods observed during these HTTP communications.

**We observed most of the requests coming to our server through the POST request, as shown below.**
![[splunk22.png]]

**To see what kind of traffic is coming through the POST requests, we will narrow down on the field `http_method=POST` as shown below:**
**Search Query:** `index=botsv1 sourcetype=stream:http dest_ip="192.168.250.70" http_method=POST`
![[splunk23.png]]
   - ﻿The result in the **src_ip** field shows two IP addresses sending all the POST requests to our server.

**Interesting fields:** In the left panel, we can find some interesting fields containing valuable information. Some of the fields are:
- src_ip
- form_data
- http_user_agent
- uri
![[int_fields.gif]]
   - The term Joomla is associated with the webserver found in a couple of fields like **uri, uri_path, http_referrer**, etc. This means our webserver is using Joomla CMS (Content Management Service) in the backend.
   - A little search on the internet for the admin login page of the Joomla CMS will show as -> `/joomla/administrator/index.php`

**It is important because this uri contains the login page to access the web portal therefore we will be examining the traffic coming into this admin panel for a potential brute-force attack.**
![[splunk24.png]]

**We can narrow down our search to see the requests sent to the login portal using this information.**
**Search query:** `index=botsv1 imreallynotbatman.com sourcetype=stream:http dest_ip="192.168.250.70"  uri="/joomla/administrator/index.php"`
**Query Explanation:** We are going to add `uri="/joomla/administrator/index.php"` in the search query to show the traffic coming into this URI.
![[splunk25.png]]
   - `form_data` The field contains the requests sent through the form on the admin panel page, which has a login page.

**We suspect the attacker may have tried multiple credentials in an attempt to gain access to the admin panel. To confirm, we will dig deep into the values contained within the form_data field, as shown below:**

**Search Query:** `index=botsv1 sourcetype=stream:http dest_ip="192.168.250.70" http_method=POST uri="/joomla/administrator/index.php" | table _time uri src_ip dest_ip form_data`
**Query Explanation:** We will add this -> `| table _time uri src dest_ip form_data` to create a table containing important fields as shown below:
![[splunk26.png]]
   - If we keep looking at the results, we will find two interesting fields `username` that includes the single username `admin` in all the events and another field `passwd` that contains multiple passwords in it, which shows the attacker from the IP `23.22.63.114` Was trying to guess the password by brute-forcing and attempting numerous passwords.
   - The time elapsed between multiple events also suggests that the attacker was using an automated tool as various attempts were observed in a short time.  

## Extracting Username and Passwd Fields using Regex
   - Looking into the logs, we see that these fields are not parsed properly. Let us use **Regex** in the search to extract only these two fields and their values from the logs and display them.
   - We can display only the logs that contain the **username** and **passwd** values in the form_data field by adding `form_data=*username*passwd*` in the above search.

**Search Query:** `index=botsv1 sourcetype=stream:http dest_ip="192.168.250.70" http_method=POST uri="/joomla/administrator/index.php" form_data=*username*passwd* | table _time uri src_ip dest_ip form_data`
![[splunk27.png]]
   - It's time to use Regex **(regular expressions)** to extract all the password values found against the field passwd in the logs. To do so, Splunk has a function called rex.
   - If we type rex it in the search head, it will show detail and an example of how to use it to extract the values.

![[splunk28.png]]
   - Now, let's use Regex.  **`rex field=form_data "passwd=(?<creds>\w+)"`** To extract the **passwd** values only.
   - This will pick the **form_data** field and extract all the values found with the field. **`creds`**.

**Search Query:**`index=botsv1 sourcetype=stream:http dest_ip="192.168.250.70" http_method=POST form_data=*username*passwd* | rex field=form_data "passwd=(?<creds>\w+)"  | table src_ip creds`
![[rex_func_splunk.gif]]
   - We have extracted the passwords being used against the username admin on the admin panel of the webserver.

**If we examine the fields in the logs, we will find two values against the field`http_user_agent` as shown below:**
![[splunk29.png]]
   - The first value clearly shows attacker used a python script to automate the brute force attack against our server.
   - But one request came from a Mozilla browser. WHY? To find the answer to this query, let's slightly change to the about search query and add `http_user_agent` a field in the search head.

**Let's create a table to display key fields and values by appending -> `| table _time src_ip uri http_user_agent creds` in the search query as shown below.**

**Search Query:** `index=botsv1 sourcetype=stream:http dest_ip="192.168.250.70" http_method=POST form_data=*username*passwd* | rex field=form_data "passwd=(?<creds>\w+)" |table _time src_ip uri http_user_agent creds`
![[splunk30.png]]
   - This result clearly shows a continuous brute-force attack attempt from an IP **23.22.63.114** and 1 password attempt **batman** from IP **40.80.148.42** using the Mozilla browser.

1. **What was the URI which got multiple brute force attempts?**
   Ans - /joomla/administrator/index.php

2. **Against which username was the brute force attempt made?**
Ans - admin

3. What was the correct password for admin access to the content management system running **imreallynotbatman.com**?
```sh
index=botsv1 sourcetype=stream:http dest_ip="192.168.250.70" http_method=POST form_data=*username*passwd*  
src_ip="40.80.148.42" | rex field=form_data “passwd=(?<creds>\w+)” | table src_ip creds status
```

![[splunk31.png]]
Ans - batman

4. **How many unique passwords were attempted in the brute force attempt?**
Ans - 