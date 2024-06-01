### What is SIEM
   - SIEM stands for **Security Information and Event Management system**.
   - It is a tool that collects data from various endpoints/network devices across the network, stores them at a centralized place, and performs correlation on them.

![[siem1.png]]

##### 1. Host-Centric Log Sources
   - These are log sources that capture events that occurred within or related to the host.
   - Some log sources that generate host-centric logs are Windows Event logs, Sysmon, Osquery, etc.
   - Some examples of host-centric logs are:
	   - A user accessing a file
	   - A user attempting to authenticate.
	   - A process Execution Activity
	   - A process adding/editing/deleting a registry key or value.
	   - Powershell execution

##### 2. Network-Centric Log Sources
   - Network-related logs are generated when the hosts communicate with each other or access the internet to visit a website.
   - Some network-based protocols are SSH, VPN, HTTP/s, FTP, etc. Examples of such events are:
	   - SSH connection
	   - A file being accessed via FTP
	   - Web traffic
	   - A user accessing company's resources through VPN.
	   - Network file sharing Activity

### Importance of SIEM
   It not only takes logs from various sources in real-time but also provides the ability to correlate between events, search through the logs, investigate incidents and respond promptly.
   
Some key features provided by SIEM are:
   - Real-time log Ingestion
   - Alerting against abnormal activities  
   - 24/7 Monitoring and visibility
   - Protection against the latest threats through early detection
   - Data Insights and visualization
   - Ability to investigate past incidents.

## Log Sources and Log Ingestion
   Some common devices that are found in a network environment are discussed below:

### Windows Machine
   - Windows records every event that can be viewed through the Event Viewer utility.
   - It assigns a unique ID to each type of log activity, making it easy for the analyst to examine and keep track of.
   - To view events in a Windows environment, type `Event Viewer` in the search bar.
   - These logs from all windows endpoints are forwarded to the SIEM solution for monitoring and better visibility.
![[logs.gif]]

## Linux Workstation
   - Linux OS stores all the related logs, such as events, errors, warnings, etc. Which are then ingested into SIEM for continuous monitoring.
   - Some of the common locations where Linux store logs are:
	   - /var/log/httpd : Contains HTTP Request  / Response and error logs.
	   - /var/log/cron   : Events related to cron jobs are stored in this location.
	   - /var/log/auth.log and /var/log/secure : Stores authentication related logs.  
	   - /var/log/kern : This file stores kernel related events.

Here is a sample of a cron log:
```txt
May 28 13:04:20 ebr crond[2843]: /usr/sbin/crond 4.4 dillon's cron daemon, started with loglevel notice  
May 28 13:04:20 ebr crond[2843]: no timestamp found (user root job sys-hourly)  
May 28 13:04:20 ebr crond[2843]: no timestamp found (user root job sys-daily)  
May 28 13:04:20 ebr crond[2843]: no timestamp found (user root job sys-weekly)  
May 28 13:04:20 ebr crond[2843]: no timestamp found (user root job sys-monthly)  
Jun 13 07:46:22 ebr crond[3592]: unable to exec /usr/sbin/sendmail: cron output for user root job sys-daily to /dev/null
```

### Web Server
   - It is important to keep an eye on all the requests/responses coming in and out of the webserver for any potential web attack attempt.
   - In Linux, common locations to write all apache related logs are /var/log/apache or /var/log/httpd.
   - Here is an example of Apache Logs:
```txt
192.168.21.200 - - [21/March/2022:10:17:10 -0300] "GET /cgi-bin/try/ HTTP/1.0" 200 3395
127.0.0.1 - - [21/March/2022:10:22:04 -0300] "GET / HTTP/1.0" 200 2216
```

### Log Ingestion
   - All these logs provide a wealth of information and can help in identifying security issues.
   - Each SIEM solution has its own way of ingesting the logs. Some common methods used by these SIEM solutions are explained below:
   
![[siem_intro.png]]
1) Agent / Forwarder:
	- These SIEM solutions provide a lightweight tool called an agent (forwarder by Splunk) that gets installed in the Endpoint.
	- It is configured to capture all the important logs and send them to the SIEM server.

2) Syslog:
	- Syslog is a widely used protocol to collect data from various systems like web servers, databases, etc., are sent real-time data to the centralized destination.

3) Manual Upload:
	- Some SIEM solutions, like Splunk, ELK, etc., allow users to ingest offline data for quick analysis. 
	- Once the data is ingested, it is normalized and made available for analysis.

4) Port-Forwarding:
	- SIEM solutions can also be configured to listen on a certain port, and then the endpoints forward the data to the SIEM instance on the listening port.

An example of how Splunk provides various methods for log Ingestion is shown below:
![[splunk_ex.png]]

## Why SIEM?
   - SIEM is used to provide correlation on the collected data to detect threats. Once a threat is detected, or a certain threshold is crossed, an alert is raised. This alert enables the analysts to take suitable actions based on the investigation.

## SIEM Capabilities
   - SIEM is one major component of a Security Operations Center (SOC) ecosystem, as illustrated below.
   - Some of the common capabilities of SIEM are:
	   - Correlation between events from different log sources.
	   - Provide visibility on both Host-centric and Network-centric activities.
	   - Allow analysts to investigate the latest threats and timely responses.
	   - Hunt for threats that are not detected by the rules in place.

![[siem2.png]]
## SOC Analyst Responsibilities
   SOC Analysts utilize SIEM solutions in order to have better visibility of what is happening within the network. 
   - Some of their responsibilities include:
	   - Monitoring and Investigating.
	   - Identifying False positives.
	   - Tuning Rules which are causing the noise or False positives.
	   - Reporting and Compliance.
	   - Identifying blind spots in the network visibility and covering them.

