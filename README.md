# Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks

# Index 
[Blueprint of your Project](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/edit/main/README.md#blueprint-of-your-project)

[Creating a Virtual Machine](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/edit/main/README.md#creating-a-virtual-machine)

[Creating & configuring a Log Analytics Workspace](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/edit/main/README.md#creating--configuring-a-log-analytics-workspace)

[Microsoft Defender for Cloud](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/edit/main/README.md#microsoft-defender-for-cloud)

[Connecting Log Analytics Workspace to Virtual Machine](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/edit/main/README.md#connecting-log-analytics-workspace-to-virtual-machine)

[Microsoft Azure Sentinel](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/edit/main/README.md#microsoft-azure-sentinel)

[Login to your Virtual Machine](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/edit/main/README.md#login-to-your-virtual-machine)

[Geo location API](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/edit/main/README.md#geo-location-api)

[PowerShell Script](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/edit/main/README.md#powershell-script)

[Creating Custom Log](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/edit/main/README.md#creating-custom-log)

[Set up Map in Sentinel](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/edit/main/README.md#set-up-map-in-sentinel)

[How to Improve the security](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/edit/main/README.md#how-to-improve-the-security)

[Reference and Appreciation](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/edit/main/README.md#reference-and-appreciation) 

# Blueprint of your Project 
The primary goal of the project was to use Azure Sentinel to track and monitor unsuccessful attempts to log into remote desktop sessions. To retrieve location information related with the IP addresses linked to these login failures, a PowerShell script was created to interface with an API. This location data was then visually displayed on a map to provide a summary of the attempted security breaches. This initiative's main objective was to improve the organization's security posture by learning important information about the sources of these intrusion attempts. All things considered, this effort makes a substantial contribution to a more thorough understanding of security issues. 


# Creating a Virtual Machine 
  • First open Microsoft Azure on your browser

  • Select or search for Virtual machines

  • Then Select "Create" option from Top Left of the page. Here select "Azure Virtual machine"

## 1) Basics 
  • Create new resource group for this project 
    
  • Name the virtual machine 
    
  • Set the Region to your closest location (Please try to use same regions for all of the resource that we use in this lab for the purpose of performance) 
      
  • Set availability options to “No infrastructure redundancy required” 
    
  • Keep Security types as “Standard” 
    
  • We are going to use “Windows 10 Pro” iso image for our virtual machine 
    
  • Leave the Size as default 

  • Username and Password. (Use whatever you want to, we will need this when we are needed to login to our Windows machine using RDP) (Don’t keep it simple otherwise someone might brute force it while we are doing this project) 

  • Select “Allow selected ports” at Public inbound ports section 

  • Select “RDP (3389)” at Select inbound ports 

 

## 2) Networking 
    • Select “Advanced” at NIC network security group 

    • Then select “Create New” at Configure network security group 

      1. Delete the default inbound rule 

      2. Create new rule by selecting “Add an inbound rule” 

        • Change Destination port ranges to “*” 

        • Set Priority to “100” 

        • Name the rule whatever you want 

        • Click “Add” 

        • Click “OK” 

 

## 3) Now Select Review + create. Let it create the VM, meanwhile we can do other things. 


# Creating & configuring a Log Analytics Workspace 

  • Search for the “Log Analytics Workspaces” in the search bar of Azure 

  • Select “Create” or “Create log analytics workspace” 

  • Select the same resource group that you created earlier. 

  • Name it whatever you want 

  • Select the same region as you selected earlier for performance 

  • Now go to “Review + create” and select “Create” 

  • Now let the process run and we can move to next task 

 
# Microsoft Defender for Cloud 

  • Search for “Defender for Cloud” in search bar of Azure 
  
  • Open the Microsoft Defender for Cloud 

  • From menu on the left panel open “Environment Setting” from Management section 

  • Select your Azure subscription 

  • Select the Log Analytics Workspace you created 

  • In Defender plan turn on the “Foundational CSPM” and “Servers” and click on “Save” button on top left 

  • In Data collection select “All Events” and click on “Save” button on top left  

  • Now move to next Task 


# Connecting Log Analytics Workspace to Virtual Machine 

  • Again, search for the “Log Analytics Workspaces” in the search bar of Azure 

  • Select the Log Analytics Workspace you created 

  • From left menu panel select “Virtual machines (deprecated)” in Classic section 

  • Select and open your Windows VM 

  • You can see that it is not connected with your Log Analytics Workspace, so now click on “Connect” 

  • Let the process run and we can move to next task 


# Microsoft Azure Sentinel 

  • Now search for the “Microsoft Sentinel” in the search bar of Azure 

  • Now select “Create Microsoft Sentinel” 

  • Select the Log Analytics Workspace that you created so we can connect it with Microsoft Sentinel 

  • Now let's go to next task 


# Login to your Virtual Machine 

  1) Search for Virtual machine in Azure search Bar

        • Open the VM you created and copy the Public IP address so you can use it to 
          login from your own PC using “Remote Desktop Connection” application 

  2) Open the “Remote Desktop Connection” on your own Windows PC. 

        • Paste your Public IP address then click on connect 

        • Now provide username and password that you created in our first task 

  3) Open the Event Viewer 

        • If you want to check logs of your login activity you can check it in Event viewer 

        • After opening the Event Viewer select the “Windows logs” and then “Security” 

        • Now you can see all the logs 

        • But our main focus will be event Id 4625, which signifies a failed login attempt. 

        • Right now, you won’t see much action happening activity related to this event Id because we were able to successfully login to the system. But when you expose this VM to the open internet, everyone will try to brute force this VM. That’s what we want for this project so we can map the attack to get visualization. 

  4) First open Command prompt from your own computer to check if your VM is open to the internet. 

        • Use this command “ping [vm ip address] -t”  

        • If you see “Request timed out” message then you have to change the firewall rules in your VM windows machine 

  5) Search for “wf.msc” in search bar to open the Windows Firewall 

        • Now Select “Windows Defender Firewall Properties” 

        • Then turn off “Firewall state” in all sections. Turn off from “Domain Profile”, “Private Profile” and “Public Profile” 

        • Then click “Apply” 

        • The purpose of this is to get as more hits as possible from all over the world


# Geo location API 

  • For this project we are going to use https://ipgeolocation.io/ , this allows us 1000 API request for free, which is enough for the purpose of this project 

  • Open the website click on sign up 

  • Create new account using your email or use your google account to sign in 

  • After sign in go to “Dashboard” 

  • You will find “API Key”, copy and save it you will need it for in the next task 


# PowerShell Script 

  • We will use custom PowerShell script to get geo location of the IP addresses found in the Event Viewer with failed login attempt. 

  • Search for the “PowerShell ISE” in search bar of your connected Windows Virtual Machine and select “Run as administrator” 

  • Click on “New Script” button located under file option 

  • Copy and paste this custom script. [Click here](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Visual_Log_Exporter.ps1) 

  • Change the value of “$API_KEY” from the script to your own API key which you got from https://ipgeolocation.io/ website. (Note: My API key won’t work because I will delete it after finishing the project) 

  • Now run the script. You will right away see the output of the sample log that we have setup in the script. If someone tries to brute force the VM, then you will see the new data right away. But sometime it may take some time so be patient. 

  • This script will create “C:\ProgramData\failed_rdp.log” file. Copy the output from the file and save it in the file with the name “failed_rdp.log” in your own computer desktop 

  • You need to save this data in your own computer, so we can perform the next task 


# Creating Custom Log 

  • Search for the “Log Analytics Workspaces” in the search bar of Azure 

  • Select the Log Analytics Workspace you created 

  • Now select the “Tables” from Settings section 

  • Then click on “Create” and select “New custom log (MMA-based)” 

  • Now you have to select and upload that “failed_rdp.log” file that you created in your own computer 

  • Click next and go to “Collection paths”. Here select “Windows” from the dropdown under the Type section and in Path sections you can copy and paste this path “C:\ProgramData\failed_rdp.log” 

  • Click next and give name to your log. You will need this name when you want to query the data 

  • Now “Review + Create” 

  

   • If you want to test the query, go back to “Logs” and you will use your Custom log name to query the data. NOTE: It might take some time to get the log from your Windows Virtual Machine to Log Analytics Workspace 

  • To separate the Raw data in different field you can use this Custom query. [Click here](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Custom%20query.txt) 


# Set up Map in Sentinel 

  1) Create Workbook 

        • To create Workbook, open the Microsoft Sentinel 

        • Then select the Log Analytics Workspace that you created for this project. 

        • Then select “Workbook” located in Threat management section 

        • Select “Add Workbook” 

        • Here select “Edit” from top left and delete the default widgets provided by Azure by selecting “...” button on right side of the widgets 

        • Now to add our own query you can select “Add” button from bottom left of the page, then select “Add query” 

        • Now copy and paste this custom query to it. [Click here](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Custom%20query.txt) 

        • Select “Map” from the drop-down of the Visualization. 

        • Now “Run Query” and check if data is available 

          1) New section will appear on the right side 

          2) Here select “label” in Metric Label under the Metric Setting 

          3) Also change Metric Value to “event_count” located right under the Metric label 

          4) Hit “Apply” 

        • Now to save this workbook, click on “Save” button located on top left of the page.  

        • You can give any name you like to save the workbook. Select your project resource in Resource group section. Also select the same region in Location section. Then hit “Apply”


# How to Improve the security  

  1) Keep services and ports open that you need. Close all unnecessary ports and services. 

  2) Use secure services. Example: SSH instead of Telnet. HTTPS instead of HTTP.  

  3) Avoid using default Passwords and Username because when someone will try to do brute force, these credentials will be used first because its east to guess. 

  4) Use strong Password. You can use password managers to create and store your passwords. 

  5) One of the best practices is using Multi Factor Authentication.


# Reference and Appreciation 
  ### Special thanks to [Josh Madakor](https://www.youtube.com/@JoshMadakor), for providing ideas for this project.   
