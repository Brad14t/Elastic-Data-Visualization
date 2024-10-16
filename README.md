# Elastic Data Visualization


# Summary:

Through this SIEM project using Elastic, I learned how to effectively monitor and analyze security events. I gained hands-on experience detecting and responding to incidents, like failed logons, RDP connections, and user group changes. Setting up custom dashboards helped me visualize security data and understand how different filters work with event codes. I also developed skills in using KQL queries to find specific events, like admin logons from untrusted IPs. This project gave me a deeper understanding of how SOC teams investigate threats and protect networks. I now feel more confident working with SIEM tools, analyzing logs, and creating alerts. Overall, it was a great way to apply what I’ve learned in cybersecurity.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Utilities:

Elastic Security (SIEM)
Kibana
KQL (Kibana Query Language)
Windows Index Pattern
Event Codes (e.g., 4625)
RDP (Remote Desktop Protocol)
Logon Types
Privileged Access Workstations (PAW)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Walkthrough:

**Goal at the end is to have 6 custom dashboards:** 

1.	Failed logon attempts (All users)
2.	Failed logon attempts (Disabled users)
3.	Failed logon attempts (Admin users only)
4.	RDP logon for service accounts
5.	User added or removed from a local group
6.	Admin logon not from PAW (Privileged Access Workstations)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**1. Failed logon attempts (All users)**

First, inside of Elastic in a new dashboard. I make sure I am using the "windows" Index Pattern. Select the drop down and select “windows”

![image](https://github.com/user-attachments/assets/af9fd16e-ec05-44c9-b8a1-ecc49158efcf)

Next, I select ‘add a filter’. 

-Field: ‘event.code’ this specifies the identification code if one exist. 

-Operator: ‘is’ specifies this code IS the given [value]

-Value: ‘4625’ this specific code is the failed logon attempt on windows system code

![image](https://github.com/user-attachments/assets/9d3be40c-4dff-441d-8ee9-ffff64d960a4)

I got an error, if you get the below error make sure the data you are inputting, has the correct dates in the calendar. My current dates only cover the last 15 minutes. I will change that to last 15 YEARS and select Apply. Also Make sure to change to Windows Index if you haven’t already. 

![image](https://github.com/user-attachments/assets/b85048f0-be6f-4750-8b15-b8179708ce68)

![image](https://github.com/user-attachments/assets/387f4575-043c-44eb-b142-0fe0a8b8a05f)

To get the data to be visualized I will go into the ‘Rows’ section to the right. 

In the field, I will type ‘user.name.keyboard’ the ‘.keyboard’ part is important because the data becomes aggregable meaning the data is kept as one long string.

I also make sure to change the number of values to 1000 to get a larger data set.

![image](https://github.com/user-attachments/assets/eb06bc99-4a2d-4a69-b7b8-6ede6fc74f91)

![image](https://github.com/user-attachments/assets/f5f6f4af-0420-4c1a-9895-359eb7619493)

Next, I will select the ‘Metrics’ section and select ‘Count’ this will count the data and display it to my dashboard.

![image](https://github.com/user-attachments/assets/a8f48a40-0da7-4e6e-8e38-6475b564d94e)

Select ‘Count’

![image](https://github.com/user-attachments/assets/71353c1c-b74f-448c-bbb9-b44e80e9baa1)

Now the data is visualized, as we can see below.

![image](https://github.com/user-attachments/assets/7cc40972-465d-4e59-818b-f220b9098558)

I will want to see hostname of the machine in this data. 

I’ll add another ‘Row’, for the field I use ‘host.hostname.keyword’ this provides the associated host name.

![image](https://github.com/user-attachments/assets/e4eac84f-031b-4be8-8037-1e0f0584a6de)

Now we have this visualization with 3 columns. 

1. Is the Username of the user logging in.
2. 2. Is the machine hostname which the logon attempt occurred.
3. Number of attempts made.

![image](https://github.com/user-attachments/assets/bdac1e21-7f4b-48e5-9510-3f4f0696b0d4)

I will re name them, so this looks cleaner and easier to read and understand. I select the row and change the ‘Display Name’.

![image](https://github.com/user-attachments/assets/33776d58-4cdf-402b-86fd-217e5371854e)

The visualization looks clean and easy to read now. I can also sort by the user with the most login failures, by selecting the arrow next to attempts and order by descending. 

![image](https://github.com/user-attachments/assets/3af9725b-d7fa-49c8-a79e-90a38ec0351e)

1 last touch to include is the logon type:
Network, interactive, batch, service and many more.

I’ll add another row and for the field type ‘winlog.logon.type.keyword’ , 1000 values, and re name to match and I named it ‘Logon Type’.

![image](https://github.com/user-attachments/assets/6645d598-9be3-47fb-8043-5c301b1b0c29)

After I felt this visualization looks good, I will select ‘Save and return’. Then select ‘Save’ to save the dashboard. I name it something and add a quick description.

![image](https://github.com/user-attachments/assets/2e898ac3-1838-4e41-b630-d009464c646e)

Make sure to get this notification in the bottom right before exiting.

![image](https://github.com/user-attachments/assets/398304f7-05d3-40b6-8904-25238d305ddc)

I add a title to the visualization so I can easily know what it does.

![image](https://github.com/user-attachments/assets/769caf8b-6f71-4e3a-8c22-735c1a2445cb)

Final look of the visualization for failed logon attempts by all users.

![image](https://github.com/user-attachments/assets/8783bf28-4c11-44b2-a08d-ea4ad88edb84)

**2. Failed logon attempts (Disabled users)**

I will create a new visualization in the dashboard menu, by selecting ‘Create visualization’.

![image](https://github.com/user-attachments/assets/5b06d9b6-b219-49fb-94c4-25e4e8642c8e)

Same start to this visualization as the last. Select windows as the index pattern, add the ‘event.code’ is 4625 filter, to filter for failed logon attempts. 

Next add another filter, the field will be ‘winlog.event_data.SubStatus’ is ‘0xc0000072. This code indicates there was a logon attempt by a disabled user. And checks windows event data for corresponding code.

![image](https://github.com/user-attachments/assets/5513131f-c330-4926-bda8-5c54153638b6)

Add a row for username. Field: ‘user.name.keyword’ this gives us the username. Set values to 1000, and change the display name for a cleaner look.

![image](https://github.com/user-attachments/assets/78a6c5d9-478f-4cfd-ba44-46013d23b741)

To visualize the data select ‘Metrics’ and ‘count’

![image](https://github.com/user-attachments/assets/3053ad1d-2ef5-47fa-8ad6-88015f70a471)

This is what the table looks like currently. I’ll add the same hostname row as last time. 

![image](https://github.com/user-attachments/assets/0ce1c5a8-502b-4965-94f7-6791a3629467)

Now I can see the user/ users that is disabled and have tried to logon but failed, and how many times. I’ll select ‘Save and return’ then ‘Save’ to the dashboard. Once I see both my visualizations ill make sure to title the new one so I can differentiate them at a glance.

![image](https://github.com/user-attachments/assets/07e694e4-15d0-43e6-9d7a-bb0288445320)

**3. Failed logon attempts (Admin users only)**

For this visualization I will clone the first visualization I did.

![image](https://github.com/user-attachments/assets/417f183e-6778-4ea5-8555-36cfa6e92d84)

I can see the cloned one below, I will select the gear icon in the top right to edit. Select ‘Edit Lens’

![image](https://github.com/user-attachments/assets/8ce69f78-7c99-4e81-8980-b228492ebf41)

The difference between these two is, to find admin users I create a KQL query ‘user.name:admin*’ (* = all admin users) and enter it into the search bar, and select ‘Update’ to see the Admin users that have failed logon attempts.

![image](https://github.com/user-attachments/assets/774b2795-d268-471b-9235-acf813c6795d)

This visualization now shows the correct data I am looking for. Next I will save this dashboard and rename this visualization to ‘Failed logon attempts (Admin users only)

![image](https://github.com/user-attachments/assets/3fbe9a59-b31a-4cc6-a57f-7226e05893a4)

I know have 3 dashboards showing all users, admins, and disabled users. Showing me what users are failing to logon, in a clear and straight forward way.

![image](https://github.com/user-attachments/assets/81be8887-c894-4194-88cb-c32511054a32)

**4. RDP logon for service accounts**

I’ll start this visualization with ‘Create visualization’ in dashboard. 

![image](https://github.com/user-attachments/assets/4e88086b-9510-44fa-8ff1-dd0b5978c5f2)

Double check ‘windows’ is the selected index pattern, and the time of the data being input is correct.

![image](https://github.com/user-attachments/assets/3e92e5b1-6094-4a69-862e-5476860f89bc)

I add a filter for the data, field: ‘event.code’ Operator: ‘is one of’ Values: 4624, 4625.

Code 4624 = Successful logon and code 4625 =Failed logon.

![image](https://github.com/user-attachments/assets/812b2895-f492-4215-8096-b5a30528cc67)

Next, I add a filter to get the users that logon remotely.

Field: ‘winlog.logon.type’ Operator: is Value: ‘RemoteInteractive’

![image](https://github.com/user-attachments/assets/65417c5c-bf3b-406b-b8f0-a4a44b1cf5f1)

For the rows I want the username and hostname rows shown previously. I changed the name of the hostname row to ‘Connected to’ to better understand immediately.

![image](https://github.com/user-attachments/assets/754215c4-69be-49ba-983f-b8345ff149f9)

![image](https://github.com/user-attachments/assets/a40ff1c6-75e8-44f9-aa04-41284a4f00dd)

I also select ‘Count’ for the metric tab to get the data showing. And name it ‘# of Logins’. 

For this visualization I want the IP address the user connected from. To achieve this add a ‘Row’ Field: ‘related.ip.keyword’ Value: 1000 and change the name to ‘Connected from’

![image](https://github.com/user-attachments/assets/e14a6da1-2c55-444a-9388-83fdced6cf83)

Now I have a visualization for seeing users connecting remotely, how many attempts and where they are connecting from. I make sure to finish this section off by saving to the dashboard.

![image](https://github.com/user-attachments/assets/6a1b1bbf-6c4d-4357-81aa-99392c1ebbe8)

**5.	User added or removed from a local group**

For this visualization I’ll select ‘Create Visualization’ make sure I have the correct index pattern and data time frame. Then select ‘Add Filter’.

Field: ‘event.code’ Operator: is one of Value: 4732, 4733

Is one of = computer says if one of the values provided is true select it.

4732 event code is when a member is added to a security enabled local group.
4733 event code is when a member is removed from a security enabled local group.

![image](https://github.com/user-attachments/assets/9151ce36-adde-4de6-b11b-c98b90b519e1)

Next, I add another filter for the local group I want checked, for this example I am using the administrator local group.

Field: ‘group.name’ Operator: is Value: ‘administrator’

![image](https://github.com/user-attachments/assets/3370ebcf-c9ff-4d33-9795-4299b809d43b)

Next, I will work on the rows we want seen. First I create the username row as seen previously. I named this one ‘User making the changes’.

![image](https://github.com/user-attachments/assets/d92b32c3-9514-4779-bb37-9cc8eb63af04)

Then select ‘Count’ for the Metric tab to show data in table.

Next row I want to show which user was added in this event. I select a new row.

Field: ‘winlog.event_data.MemberSid.keyword’ and changed the name to ‘User added’

![image](https://github.com/user-attachments/assets/f712ee39-9cef-44a4-a4d2-74c29658e690)

Next row I want to see what group was modified. I select a new row.

Field: group.name.keyword and changed the name to ‘Group modified’

![image](https://github.com/user-attachments/assets/3ef49988-ac58-458a-afd0-0300114d5efe)

I can see now the user, who was added, where they were added, and how many times.

But I can’t see if the action and if the user was added or removed. For this, I’ll select new row.

Field: event.action.keyword and changed the name to ‘Action performed’ 

![image](https://github.com/user-attachments/assets/7cbeee85-6b95-4357-ae74-b6ba85831e7f)

One last row I want to add is the machine this action was performed on. For this I’ll select a new row.

Field: ‘host.hostname.keyword’ and changed the name to ‘Action performed on’

![image](https://github.com/user-attachments/assets/2dcc8a3a-5211-4693-a38e-fb6b7c6c9462)

This is what this visualization looks like finalized. I can see if anyone makes a change to the admin local group, what they did, where from and what kind of machine it was performed on.

![image](https://github.com/user-attachments/assets/e9271e0a-846c-4ebb-b8b3-40e5a3518cee)

I changed the name of this visualization to ‘User added or removed from a local group’ and confirm it is in my dashboard.

![image](https://github.com/user-attachments/assets/5815c5ba-7ce4-4f6b-b1f8-feaf1c7b85dd)

**6.	Admin logon not from PAW (Privileged Access Workstations)**

Next visualization I’ll start by selecting ‘Create visualization’. Then confirm I’m using the correct index pattern, and the correct time frame of data.

Next, I’ll select ‘Add filter’ 

Field: ‘event.code’ Operator: is Value: 4624 (this checks for successful logons)

![image](https://github.com/user-attachments/assets/f073e493-c5a3-4488-b004-a5b3f1f645bb)

Next I’ll add another filter for Network Logon.

Field: ‘winlog.event_data.LogonType’ Operator: is Value: 3 (3 = Network logon)

![image](https://github.com/user-attachments/assets/287a5b32-8fab-4829-b7af-de37937aed7c)

Next I’ll start setting up what data I want to see. I select a new row.

Field: ‘user.name.keyword’ changed the name to ‘User’

![image](https://github.com/user-attachments/assets/9406cdee-6417-4ac2-9d06-d694331dd2f0)

Next, I want to see what IP address the user is connecting from. I’ll select a new row.

Field: ‘source.ip.keyword’ Changed the name to ‘Connected from’.

![image](https://github.com/user-attachments/assets/70ae9486-f43e-4f57-a53a-31088e0c3e75)

Next to see the data ill select ‘Count’ in the metrics tab.

I make a KQL query to check for any admins connecting from an ip other than the trusted one.

Query: user.name:Admin* AND NOT source.ip:”192.168.28.134”

This query checks if username is in the Admin group AND NOT the secure ip given, show this data.

Once I hit enter I can see the visualization is complete and showing any admin that has logged on from a non-trusted workstation.

![image](https://github.com/user-attachments/assets/14ff8b9f-4e85-4656-b9d6-c97a66adb8de)

I make sure to save to the dashboard and change the display name in the dashboard 

I can now see it displaying in my dashboard.

![image](https://github.com/user-attachments/assets/7c988843-2264-4e1d-809d-5ed97e68ef28)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Final Dashboards:

![image](https://github.com/user-attachments/assets/64e4e189-dd1f-487f-bec1-daf0ec372280)

![image](https://github.com/user-attachments/assets/25b0bde6-4710-4ea3-9a8a-36890c5326ea)

![image](https://github.com/user-attachments/assets/b90e0c8c-5c04-4b88-acf8-5c957537987d)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Key Takeaways 

•	Learn how to monitor and analyze security events using a Security Information and Event Management (SIEM) platform (Elastic Security)

•	Gain hands-on experience in detecting, responding to, and mitigating security incidents.

•	Develop skills in analyzing logs, setting up alerts, and investigating threats within a SOC environment.

•	Build a foundational understanding of cybersecurity workflows and tools used to protect an organization’s network.












