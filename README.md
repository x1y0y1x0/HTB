# HTB
Splunk
1-) Navigate to http://[Target IP]:8000, open the "Search & Reporting" application, and find through an SPL search against all data the account name with the highest amount of Kerberos authentication ticket requests. Enter it as your answer.

**Answer:** **index=* sourcetype="WinEventLog:Security" EventCode=4768
| stats count by Account_Name**

2-) Navigate to http://[Target IP]:8000, open the "Search & Reporting" application, and find through an SPL search against all 4624 events the count of distinct computers accessed by the account name SYSTEM. Enter it as your answer.

**Answer:** **index=* EventCode=4624 Account_Name="SYSTEM"
| stats dc(ComputerName)
| eval toplam_bilgisayar=max(dc_ComputerName)**


3-) Navigate to http://[Target IP]:8000, open the "Search & Reporting" application, and find through an SPL search against all 4624 events the account name that made the most login attempts within a span of 10 minutes. Enter it as your answer.

**Answer:** **index=* EventCode=4624 
| bin _time span=10m  
| stats count by _time, Account_Name 
| stats max(count) as max_attempts by Account_Name**
