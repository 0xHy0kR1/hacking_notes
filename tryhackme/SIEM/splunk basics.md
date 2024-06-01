Splunk is one of the leading SIEM solutions in the market that provides the ability to collect, analyze and correlate the network and machine logs in real-time.

## Splunk Components
   - Splunk has three main components, namely Forwarder, Indexer, and Search Head.
![[splunk1.png]]

### Splunk Forwarder
   - Splunk Forwarder is a lightweight agent installed on the endpoint intended to be monitored.
   - Its main task is to collect the data and send it to the Splunk instance.
   - It does not affect the endpoint's performance as it takes very few resources to process.
   - Some of the key data sources are:
	- Web server generating web traffic.
	- Windows machine generating Windows Event Logs, PowerShell, and Sysmon data.
	- Linux host generating host-centric logs.
	- Database generating DB connection requests, responses, and errors.

![[splunk2.png]]
### Splunk Indexer
   - Splunk Indexer plays the main role in processing the data it receives from forwarders.
   - It takes the data, normalizes it into field-value pairs, determines the datatype of the data, and stores them as events. Processed data is easy to search and analyze.


![[splunk3.png]]
### Search Head
   - Splunk Search Head is the place within the Search & Reporting App where users can search the indexed logs as shown below.
   - When the user searches for a term or uses a Search language known as Splunk Search Processing Language, the request is sent to the indexer and the relevant events are returned in the form of field-value pairs.
![[splunk4.png]]

**Search Head also provides the ability to transform the results into presentable tables, visualizations like pie-chart, bar-chart and column-chart, as shown below:**
![[splunk5.png]]

## Splunk Bar
   - When you access Splunk, you will see the default home screen identical to the screenshot below.
![[splunk6.png]]

**The top panel is the **Splunk Bar** (below image).**
![[splunk7.png]]
   - In the Splunk Bar, you can see system-level messages (**Messages**)
   - configure the Splunk instance (**Settings**)
   - review the progress of jobs (**Activity**)
   - miscellaneous information such as tutorials (**Help**)
   - a search feature (**Find**).

**The ability to switch between installed Splunk apps instead of using the **Apps panel** can be achieved from the Splunk Bar, like in the image below.**
![[splunk8.png]]

### Apps Panel
   - Next is the **Apps Panel**.  In this panel, you can see the apps installed for the Splunk instance.
   - The default app for every Splunk installation is **Search & Reporting**.
![[tryhackme/SIEM/images/splunk9.png]]

### Explore Splunk
   - This panel contains quick links to add data to the Splunk instance, add new Splunk apps, and access the Splunk documentation.
    ![[splunk10.png]]

### Splunk Dashboard
   - The last section is the **Home Dashboard**.
   - By default, no dashboards are displayed. You can choose from a range of dashboards readily available within your Splunk instance.
   - You can select a dashboard from the dropdown menu or by visiting the **dashboards listing page**.
![[splunk-dash.gif]]

   - You can also create dashboards and add them to the Home Dashboard.
   - The dashboards you create can be viewed isolated from the other dashboards by clicking on the **Yours** tab.

**Below is a chart listing from the Splunk documentation detailing each data source category.**
![[splunk11.png]]

**We will use the Upload Option to upload the data from our local machine.**
As shown above, it has a total of 5 steps to successfully upload the data.
1. **Select Source** -> Where we select the Log source.
2. **Select Source Type** -> Select what type of logs are being ingested.
3. **Input Settings** ->Select the index where these logs will be dumped and hostName to be associated with the logs.  
4. **Review** -> Review all the gif  
5. **Done** -> Final step, where the data is uploaded successfully and ready to be analyzed.

![[splunk-data-upload.gif]]

Download the attached log file "VPN_logs" and upload this file into the Splunk instance with the right source type.

##### 1. Upload the data attached to this task and create an index "VPN_Logs". How many events are present in the log file?
Ans - 2862
![[splunk-que1.webp]]

##### 2. How many log events by the user **Maleena** are captured?
Ans - 60
##### 3. What is the name associated with IP 107.14.182.38?
Ans - Smith
![[splunk-que3.webp]]

##### 4. What is the number of events that originated from all countries except France?
Ans - 2814
![[splunk-que4.webp]]

##### 5. How many VPN Events were observed by the IP 107.3.206.58?
Ans - 14
![[splunk-que5.webp]]

