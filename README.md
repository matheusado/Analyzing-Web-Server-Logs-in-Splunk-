<h1>Analyzing-Web-Server-Logs-in-Splunk</h1>


<h2>Description</h2>
This project demonstrates the use of Splunk Enterprise to analyze and secure web server logs. It includes parsing and indexing log data from multiple server hosts to identify HTTP status trends, detect anomalies in IP activity, monitor for missing resources, and spot potential security breaches such as SQL injection attempts. The project leverages SPL queries and visualizations to enhance situational awareness and strengthen network defense capabilities.
<br />


<h2>Languages and Utilities Used</h2>

- SPL (Search Processing Language)
- Splunk Enterprise
- Github (dataset source)
- 7-Zip (for dataset extraction)
- Web browser (for Splunk UI access)
- Windows 11 Pro

<h2>Environments Used </h2>

- macOS Ventura 13.7.4 (21H2)
- Windows 11 Pro

<h2>Program walk-through:</h2>

<p align="center">
Sign in with your administrator credentials on Splunk: <br/>
<img src="https://i.imgur.com/cA49qNy.png"/>
<br />
<br />
Paste the link given below in the browser and press enter: 

https://drive.google.com/file/d/1XGUTQOSstwTj3yf7vm1iCdrd0SiFlxM- /view?usp=sharing   <br/>
<img src="https://i.imgur.com/X927srf.png"/>
<br />
<br />
Click on Download icon: <br/>
<img src="https://i.imgur.com/OtVmjgK.png"/>
<br />
<br />
Navigate to Splunk home page and click on Settings:  <br/>
<img src="https://i.imgur.com/G1b24Bq.pngg"/>
<br />
<br />
Now, click on Add Data:  <br/>
<img src="https://i.imgur.com/HL78Knr.png"/>
<br />
<br />
Scroll down and click on Upload:  <br/>
<img src="https://i.imgur.com/Iddk71i.png"/>
<br />
<br />
Click on Select File:  <br/>
<img src="https://i.imgur.com/Amjg1F1.png"/>
<br />
<br />
Select apache_security_logs.csv file and click on Open:  <br/>
<img src="https://i.imgur.com/mxJ4BVX.png"/>
<br />
<br />
Click on Next:  <br/>
<img src="https://i.imgur.com/Rp6c0tm.png"/> 
<br />
<br />
Then, click on Next again: <br/>
<img src="https://i.imgur.com/XrKyl6x.png"/>
<br />
<br />
Enter apache-logs in Host field value and click on Create a new index:  <br/>
<img src="https://i.imgur.com/3xiHb99.png"/>
<br />
<br />
Enter sec-logs as Index Name and click on Save:  <br/>
<img src="https://i.imgur.com/hMXwgVo.png"/>
<br />
<br />
Click on Review:  <br/>
<img src="https://i.imgur.com/oLhKEf2.png"/>
<br />
<br />
Click on Submit:  <br/>
<img src="https://i.imgur.com/TCDqL6r.pn"/>
<br />
<br />
Click on Start Searching:  <br/>
<img src="https://i.imgur.com/ruzwfh8.png"/>
<br />
<br />
Now, Analyze the log using SPL queries. Enter the following query in the search box and click on the search icon: 

index=sec-logs host=apache-logs | stats count by Status  <br/>

<img src="https://i.imgur.com/jyJtjzU.png"/>

Note: This query groups logs by HTTP status code and counts the number of occurrences for each status. 
<br />
<br />
Enter the following query in the search box and click on the search icon: 

index=sec-logs host=apache-logs | stats count by "IP Address" | sort - count   <br/>

<img src="https://i.imgur.com/GeL3QEx.png"/>

Note: This query groups logs by unique IP addresses, counts the occurrences for each IP address, and sorts the results in descending order based on the count. 
<br />
<br />
Enter the following query in the search box and click on the search icon: 

index=sec-logs host=apache-logs Status=404 | top limit=5 Resource 

<img src="https://i.imgur.com/p7QuChc.png"/>

Note: This query identifies the top 5 most frequently requested resources that resulted in "Not Found" errors and lists them based on their occurrence frequency. 
<br />
<br />
Enter the following query in the search box and click on the search icon: 

index=sec-logs host=apache-logs "Breach Message"="SQL Injection attempt detected" | timechart span=1d count 

<img src="https://i.imgur.com/fUKAvH8.png"/>

Note: This query filters logs for SQL injection attempt alerts and creates a time-based chart that counts these events daily, grouping them into 1-day intervals. 
<br />
<br />
Enter the following query in the search box and click on the search icon: 

index=sec-logs host=apache-logs Status=403 | stats count by Method 

<img src="https://i.imgur.com/UMmjwhi.png"/>

Note: This query groups logs by HTTP method where the status is 403 (Forbidden) and counts the occurrences of each method. 
<br />
<br />
Enter the following query in the search box and click on the search icon: 

index=sec-logs host=apache-logs | stats count by "User Agent" | sort – count 

<img src="https://i.imgur.com/pDagAl3.png"/>

Note: This query groups logs by the "User Agent" field, counts the occurrences of each user agent, and sorts the results in descending order based on the count. 
<br />
<br />
Enter the following query in the search box and click on the search icon: 

index=sec-logs host=apache-logs | stats count by "Breach Message" | sort - count 

<img src="https://i.imgur.com/hs3EAlA.png"/>

Note: This query groups logs by the "Breach Message" field, counts the occurrences of each breach message, and sorts the results in descending order based on the count. 
<br />
<br />
Enter the following query in the search box and click on the search icon: 

index=sec-logs host=apache-logs Status=500 | stats count by "IP Address" | sort – count 

<img src="https://i.imgur.com/V9Ub7Vy.png"/>

Note: This query filters for logs with a Status of 500 (Internal Server Error), groups them by IP address, counts the occurrences of each IP address, and sorts the results in descending order based on the count. 
<br />
<br />
Enter the following query in the search box and click on the search icon: 

index=sec-logs host=apache-logs Resource="/admin" | top limit=3 "IP Address" 

<img src="https://i.imgur.com/WF1ddGg.png"/>

Note: This query is for identifying the top three most frequently accessed /admin resource on an Apache server by IP addresses, highlighting potential security concerns. 
<br />
<br />
Enter the following query in the search box and click on the search icon: 

index=sec-logs host=apache-logs "Breach Message"="Directory traversal attack" | stats dc(Resource) as unique_resources 

<img src="https://i.imgur.com/BexDVLc.png"/>

Note: This query filters for logs indicating a "Directory traversal attack", calculates the distinct number of unique resources targeted during these attacks, and labels the result as unique resources. 
<br />
<br />
Enter the following query in the search box and click on the search icon: 

index=sec-logs host=apache-logs | stats dc("Breach Message") as distinct_breaches by "IP Address" | sort - distinct_breaches desc | head 5 

<img src="https://i.imgur.com/2NR5V1p.png"/>

Note: This query groups logs by IP address, calculates the number of distinct breach message types associated with each IP address, and displays the top 5 IP addresses with the highest counts, sorted in descending order. 
<br />
<br />
Enter the following query in the search box and click on the search icon: 

index=sec-logs host=apache-logs | eval success=if(Status=200, 1, 0) | eval failure=if(Status>=400 and Status<600, 1, 0) | stats sum(success) as successful, sum(failure) as unsuccessful by Method | eval ratio=round(successful/unsuccessful, 2) 

<img src="https://i.imgur.com/Lym5gS8.png"/>

Note: This query calculates the ratio of successful HTTP responses (Status 200) to unsuccessful responses (Status 400-599) for each HTTP method and rounds the ratio to two decimal places for clarity. 
<br />
<br />
Enter the following query in the search box and click on the search icon: 

index=sec-logs host=apache-logs "Breach Message"="SQL Injection attempt detected" OR "Breach Message"="Cross-Site Scripting (XSS) attack" | stats dc("Breach Message") as breach_count by "IP Address" | where breach_count > 1 

<img src="https://i.imgur.com/jq5kliv.png"/>

Note: This query calculates the ratio of successful HTTP responses (Status 200) to unsuccessful responses for each HTTP method and rounds the ratio to two decimal places for clarity. 
<br />
<br />
Enter the following query in the search box and click on the search icon: 

index=sec-logs host=apache-logs Resource="/secure" | stats min(_time) as earliest_time, max(_time) as latest_time | eval earliest_time=strftime(earliest_time, "%Y-%m-%d %H:%M:%S"), latest_time=strftime(latest_time, "%Y-%m-%d %H:%M:%S") 

<img src="https://i.imgur.com/Dj6ATXj.png"/>

Note: This query filters logs where the Resource field equals "/secure", calculates the earliest and latest timestamps, and converts these timestamps from Unix epoch format to a human-readable date and time format. 
<br />
<br />
Enter the following query in the search box and click on the search icon: 

index=sec-logs host=apache-logs | eventstats count as total_events | stats count as breach_count by "Breach Message" | eval percentage=round((breach_count/total_events)*100, 2) | sort – percentage 

<img src="https://i.imgur.com/EPMTI3R.png"/>

Note: This query calculates the total number of events, groups the events by the "Breach Message" field, counts the number of events for each breach type, calculates the percentage of each breach type relative to the total events, and sorts the breach types in descending order of their percentages. 
<br />
<br />
Enter the following query in the search box and click on the search icon: 

index=sec-logs host=apache-logs | transaction "IP Address" startswith=(Status=403) endswith=(Status=200) | table "IP Address", duration, eventcount 

<img src="https://i.imgur.com/HTu4WxK.png"/>

Note: This query calculates the total number of events, groups the events by the "Breach Message" field, counts the number of events for each breach type, calculates the percentage of each breach type relative to the total events, and sorts the breach types in descending order of their percentages. 
<br />
<br />
Enter the following query in the search box and click on the search icon: 

index=sec-logs host=apache-logs Status=403 | stats count by Resource, Method | sort - count | head 3 

<img src="https://i.imgur.com/IItT9UF.png"/>

Note: This query filters for logs with a Status of 403 (Forbidden), groups the data by the combination of Resource and Method, counts the occurrences of each combination, sorts the results in descending order of the count, and displays the top 3 most frequent combinations. 
<br />
<br />
Enter the following query in the search box and click on the search icon: 

index=sec-logs host=apache-logs | stats count by "User Agent", Resource | sort - count | head 1 

<img src="https://i.imgur.com/qfaH0Zu.png"/>

Note: This query groups log entries by the combination of User Agent and Resource, counts the occurrences of each combination, sorts the results in descending order of frequency, and displays the most frequent combination. 
<br />
<br />
Enter the following query in the search box and click on the search icon: 

index=sec-logs host=apache-logs | stats count by "Breach Message", Status | xyseries "Breach Message", Status, count 

<img src="https://i.imgur.com/NvS4Kl1.png"/>

Note: This query groups log entries by the combination of Breach Message and Status fields, counts the number of events for each combination, and formats the output into a matrix where each row represents a Breach Message, each column represents a Status, and the cell values represent the count of events. 
<br />
<br />
Enter the following query in the search box and click on the search icon: 

index=sec-logs host=apache-logs "Breach Message"="SQL Injection attempt detected" | stats count by "IP Address" | sort - count | head 10 

<img src="https://i.imgur.com/lvo2dM8.png"/>

Note: This query filters for logs indicating an "SQL Injection attempt detected", groups them by IP Address, counts the number of SQL injection attempts for each IP address, sorts the results in descending order of frequency, and displays the top 10 IP addresses with the highest counts. 
<br />
<br />
Enter the following query in the search box and click on the search icon: 

index=sec-logs host=apache-logs | chart count by Resource, Method 

<img src="https://i.imgur.com/putScGy.png"/>

Note: This query groups log entries by Resource and Method, counts the number of events for each combination, and organizes the output into a table or chart format where Resource is represented as rows, Method as columns, and the count of events populates the cells. 
<br />
<br />
Enter the following query in the search box and click on the search icon: 

index=sec-logs host=apache-logs | timechart span=1d count by Breach_Message | head 3 

<img src="https://i.imgur.com/1HMM8Om.png"/>

Note: This query groups logs into 1-day intervals, counts the number of events for each day organized by Breach Message, and limits the output to the first 3 rows. 

Conclusion:
This project successfully demonstrated the power of Splunk Enterprise in analyzing and visualizing web server log data for enhanced security monitoring. By uploading and configuring a comprehensive dataset, we developed and executed advanced SPL queries to identify critical patterns such as HTTP status anomalies, suspicious IP address behavior, and breach activity including SQL injection and directory traversal attempts. The project enabled us to detect potential threats, gain visibility into access trends, and generate actionable insights through dashboards and time-based visualizations.
Overall, this hands-on experience provided valuable skills in using Splunk for log analysis, improved our understanding of network traffic behavior, and highlighted how centralized logging tools can enhance the detection and response capabilities of modern cybersecurity environments.

<br />
<br />
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
