# Elastic-Data-Visualization


# Summary:

Through this SIEM project using Elastic, I learned how to effectively monitor and analyze security events. I gained hands-on experience detecting and responding to incidents, like failed logons, RDP connections, and user group changes. Setting up custom dashboards helped me visualize security data and understand how different filters work with event codes. I also developed skills in using KQL queries to find specific events, like admin logons from untrusted IPs. This project gave me a deeper understanding of how SOC teams investigate threats and protect networks. I now feel more confident working with SIEM tools, analyzing logs, and creating alerts. Overall, it was a great way to apply what I’ve learned in cybersecurity.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Walkthrough:

**Goal at the end is to have 6 custom dashboards:** 

1.	Failed logon attempts (All users)
2.	Failed logon attempts (Disabled users)
3.	Failed logon attempts (Admin users only)
4.	RDP logon for service accounts
5.	User added or removed from a local group
6.	Admin logon not from PAW (Privileged Access Workstations)

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**1. Failed logon attempts (All users)**

First, inside of Elastic in a new dashboard. I make sure I am using the windows Index Pattern. Select the drop down and select “windows”






