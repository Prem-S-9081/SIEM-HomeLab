**SIEM HOME LAB – PREM PERSONAL NETWORK**
I have assembled a home lab using a Kali virtual machine and Elastic SIEM. I used the Elastic Beats agent to transfer data from the Kali virtual machine to the SIEM; Nmap was used to generate security events on the Kali VM; and the Elastic web interface was used to query and analyze the logs in the SIEM. In order to detect security incidents, I also designed an alert and a dashboard to visualize security occurrences.
Using the help of this home lab, I can acquire and hone the skills required for efficient security monitoring and incident response using Elastic SIEM. By following these steps, I can enhance my security monitoring abilities and obtain practical experience with utilizing a SIEM, which will help me become a great security analyst or engineer.	

**Prerequisites**
Before we get started, make sure you have the following:
1.	VirtualBox or VMware
2.	Basic knowledge of Linux and virtualization software.	

**Overview of the tasks**
•	Set up a free Elastic account.
•	Install the Kali VM.
•	Set up the Linux virtual machine's Elastic Agent to gather logs and send them to the SIEM.
•	Generate security events on the Kali VM.
•	Query to find the security events in the Elastic SIEM.
•	Create a Dashboard to visualize security events.
•	Create alerts for security events.	

**Task 1: Set up an Elastic Account**
1.	Sign up for a free trial to use Elastic Cloud at https://cloud.elastic.co/registration
2.	Once you have an Elastic account, log in to the Elastic Cloud console at https://cloud.elastic.co.
3.	Click on “Start your free trial.”
4.	When choosing the deployment type, click the "Create Deployment" button and choose "Elasticsearch."
5.	Select the deployment size and region that best suit your requirements, then click "Create Deployment."
6.	Wait for the configuration to complete.
7.	Once the deployment is ready, click “continue.”	

**Task 2: Setting up the Linux VM**
1.	Download the Kali Linux VM from the official Kali website at https://www.kali.org/get-kali/#kali-virtual-machines.
2.	Using the Kali VM file, create a new virtual machine (VM) in your favourite virtualization software, like VMware or VirtualBox.
3.	Start the VM and follow the on-screen prompts to install Kali.
4.	After installation is finished, use "kali" as the login and password to access the Kali virtual machine (VM).	

**Task 3: Setting up the Agent to Collect Logs**
To gather and transmit data to a centralized system for analysis and monitoring, software called an agent is placed on a device, such as a server or endpoint. Security-related events from your endpoints are gathered and forwarded to your Elastic SIEM instance via an agent in the context of the platform.
To set up the agent to collect logs from your Kali VM and forward them to your Elastic SIEM instance, follow these steps:
1.	To access the Integrations page, log in to your Elastic SIEM instance, click the Kibana main menu bar in the upper left corner, and then choose "Integrations" from the bottom menu.
2.	Search for “Elastic Defend” and click on it to open the integration page.
3.	To install the agent on your Kali VM, click "Install Elastic Defend" and adhere to the installation instructions on the integration page. Paste that command into the Kali terminal (command line).
4.	You will receive a notification stating that the "Elastic Agent has been successfully installed" after the agent has been installed, which may take several minutes. It may take a few minutes for the logs to show up in the SIEM, but it will begin automatically gathering and transmitting data to your Elastic SIEM server.
5.	You can verify that the agent has been installed correctly by running this command: 
sudo systemctl status elastic-agent.service
Note: Before continuing, make sure your Kali is online by pinging google.com if you receive a problem when installing the agent.
![image](https://github.com/user-attachments/assets/bd787d52-1502-4505-8ae2-04cbc2b9af60)
![image](https://github.com/user-attachments/assets/73301d79-ec26-47f9-bcdc-bff641d11cae)

**Task 4: Generating Security Events on the Kali VM**
You can create some security-related events on your Kali virtual machine (VM) to confirm that the agent is operating as intended. We can use a tool like Nmap and Wireshark to accomplish this. A free and open-source tool for network administration, exploration, and security auditing is called Nmap (Network Mapper). Its purpose is to identify hosts and services on a computer network, generating a network "map" in the process. Nmap may be used to find out what operating system and software are installed on a target system, check hosts for open ports, and obtain further network information. Wireshark is a free and open-source packet analyzer. It is used for network troubleshooting, analysis, software and communications protocol development, and education.
To run an Nmap scan, follow these steps:
1.	Install Nmap on the Linux VM if you’re not using Kali, Nmap already comes preinstalled in Kali. Open a new Terminal and run this command to install it: sudo apt-get install nmap.
2.	Run a scan on Kali machine by running the command: sudo nmap <vm-ip>. You can also run a scan of your host machine if you place your Kali VM on a “bridged” network.
3.	This scan generates several security events, such as the detection of open ports and the identification of services running on those ports. Run a few more Nmap scans (“nmap -sS <ip address>”, “nmap -sT <ip address>”, “nmap -p- <ip address>”etc..
 
**Task 5: Querying for Security Events in the Elastic SIEM**
We can now begin searching through and examining the SIEM's logs after moving data from the Kali VM.
To do this, follow these steps:
1.	To see the logs from the Kali virtual machine, within your Elastic Deployment, click the three horizontal line menu icon in the top-left corner and select the "Logs" option under "Observability."
2.	In the search bar, enter a search query to filter the logs. For example, to search for all logs related to Nmap scans, enter the query: event.action:“nmap_scan” or process.args: “sudo”.
3.	Click on the “Search” button to execute the search query.
4.	The results of the search query will be displayed in the table below. You can click on the three dots next to each event to view more details.
Note: You can learn more about how security incidents are found, looked into, and handled in real-world settings by creating and examining various security event types in Elastic SIEM, such as the one above, or by creating authentication failures caused by a user entering the wrong password or trying to log in to SSH with the wrong password.

**Task 6: Create a Dashboard to Visualize the Events**
You can also use the visualizations and dashboards in the SIEM app to analyze the logs and identify patterns or anomalies in the data.
Here’s how you can do that:
1.	Navigate to the Elastic web portal at https://cloud.elastic.co/.
2.	Click on the menu icon on the top-left, then under “Analytics,” click on “Dashboards.”
3.	Click on the “Create dashboard” button on the top right to create a new dashboard.
4.	Click on the “Create Visualization” button to add a new visualization to the dashboard.
5.	Choose the visualization kind you desire, either "Area" or "Line." A chart displaying the number of incidents over time will be produced as a result.
6.	Choose "Timestamp" for the horizontal field and "Count" for the vertical field type in the "Metrics" section of the visualization editor on the right. This will display the number of occurrences over time.
7.	Click on the “Save” button to save the visualization and then complete the rest of the settings.
 
**Task 7: Create an Alert**
Alerts are an essential component of a SIEM that help identify security events and quickly address them. Alerts can be set up to perform particular actions when predetermined criteria are fulfilled, and they can be generated using established rules or bespoke queries. 
Here are the steps:
1.	Click on the menu icon on the top-left, then under “Security,” click on “Alerts.”
2.	Click on “Manage rules” at the top right.
3.	Click on the “Create new rule” button at the top right.
4.	Under the “Define rule” section, select the “Custom query” option from the dropdown menu.
5.	Establish the rules' conditions under "Custom query." The following query can be used to find Nmap scan events. All events that match the action "nmap_scan" will be matched by this query. Next, select "Continue."
6.	Under the “About rule” section, give your rule a name and a description (Nmap Scan Detection).
7.	You can prioritize warnings according to their importance by setting the alert's severity level. Click "Continue" after maintaining all other default settings under "Schedule rule."
8.	Choose the action you wish to perform when the rule is activated from the "Actions" section. You have the option to start a custom webhook, start a Slack chat, or send an email notification.
9.	Finally, click the “Create and enable rule” button to create the alert.
Note: After creating the alert, it will keep an eye out for Nmap scan events in your logs. The alarm will sound and the chosen action will be carried out if a Nmap scan event is found. Under "Security," go to the "Alerts" section to view and manage your notifications.
 
**Additional Observations :**
•	In order to use Anomaly detection, Data Frame Analytics, Dashboard Management, Data Visualizations, and other features on your deployment, you can also build Machine Learning models.

•	You may locate your rule operating on the specified path and receiving the triggered actions on the main dashboard under the alerts part of the observability section. 

•	You can filter out specific events from the stream section by using the timestamps and actions completed as a collaborative log found in the discover sections. These logs will be used to create a pictorial representation of the occurrences.
 
•	Numerous performance data, like CPU Usage, CPU Credits, Number of Inbound Requests, Search Response Time, and so forth, are available on your deployment's Main Page. You will receive a comprehensive analysis of the performance and health of your deployment from these indicators. 
 
•	You can compute your data quality, Kubernetes, entity analytics, and detection and response data using a variety of pre-defined dashboards found under the security area. Additionally, you may design a custom dashboard to track the actions that are triggered by your deployment and conduct technical analysis.
 
 

