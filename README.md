# Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks

<br>

## Index 
[Blueprint of your Project](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/tree/main?tab=readme-ov-file#blueprint-of-your-project)

[Creating a Virtual Machine](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/tree/main?tab=readme-ov-file#creating-a-virtual-machine)

[Creating & configuring a Log Analytics Workspace](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/tree/main?tab=readme-ov-file#creating--configuring-a-log-analytics-workspace)

[Microsoft Defender for Cloud](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/tree/main?tab=readme-ov-file#microsoft-defender-for-cloud)

[Connecting Log Analytics Workspace to Virtual Machine](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/tree/main?tab=readme-ov-file#connecting-log-analytics-workspace-to-virtual-machine)

[Microsoft Azure Sentinel](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/README.md#microsoft-azure-sentinel)

[Login to your Virtual Machine](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/README.md#login-to-your-virtual-machine)

Geo location API

[PowerShell Script](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/edit/main/README.md#powershell-script)

[Creating Custom Log](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/edit/main/README.md#creating-custom-log

[Set up Map in Sentinel](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/edit/main/README.md#set-up-map-in-sentinel)

[How to Improve the security](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/edit/main/README.md#how-to-improve-the-security)

[Reference and Appreciation](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/edit/main/README.md#reference-and-appreciation) 

<br>

## Blueprint of your Project 
The primary goal of the project was to use Azure Sentinel to track and monitor unsuccessful attempts to log into remote desktop sessions. To retrieve location information related with the IP addresses linked to these login failures, a PowerShell script was created to interface with an API. This location data was then visually displayed on a map to provide a summary of the attempted security breaches. This initiative's main objective was to improve the organization's security posture by learning important information about the sources of these intrusion attempts. All things considered, this effort makes a substantial contribution to a more thorough understanding of security issues. 

<br>

## Creating a Virtual Machine 
  • First open Microsoft Azure on your browser

  • Select or search for Virtual machines

  • Then Select "Create" option from Top Left of the page. Here select "Azure Virtual machine"

### 1) Basics 
  • Create new resource group for this project 
    
  • Name the virtual machine 
    
  • Set the Region to your closest location (Please try to use same regions for all of the resource that we use in this lab for the purpose of performance) 
      
  • Set availability options to “No infrastructure redundancy required” 
    
  • Keep Security types as “Standard” 
    
  • We are going to use “Windows 10 Pro” iso image for our virtual machine 

<p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20204446.png"></p>
    
  • Leave the Size as default 

  • Username and Password. (Use whatever you want to, we will need this when we are needed to login to our Windows machine using RDP) (Don’t keep it simple otherwise someone might brute force it while we are doing this project) 

  • Select “Allow selected ports” at Public inbound ports section 

  • Select “RDP (3389)” at Select inbound ports 

<p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20204504.png"></p>

### 2) Networking 
    • Select “Advanced” at NIC network security group 

    • Then select “Create New” at Configure network security group
<p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20204633.png"></p>
      1. Delete the default inbound rule 

      2. Create new rule by selecting “Add an inbound rule” 

        • Change Destination port ranges to “*” 

        • Set Priority to “100” 

        • Name the rule whatever you want 

        • Click “Add” 

        • Click “OK” 

<p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20204832.png"></p>
 

### 3) Now Select Review + create. Let it create the VM, meanwhile we can do other things. 

<br>

## Creating & configuring a Log Analytics Workspace 

  • Search for the “Log Analytics Workspaces” in the search bar of Azure 

  • Select “Create” or “Create log analytics workspace” 
  
<p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20205157.png"></p>

  • Select the same resource group that you created earlier. 

  • Name it whatever you want 

  • Select the same region as you selected earlier for performance 

  • Now go to “Review + create” and select “Create” 
<p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20205327.png"></p>

  • Now let the process run and we can move to next task 

  <br>
  
## Microsoft Defender for Cloud 

  • Search for “Defender for Cloud” in search bar of Azure 
  
  • Open the Microsoft Defender for Cloud 

  • From menu on the left panel open “Environment Setting” from Management section 

  • Select your Azure subscription 

  • Select the Log Analytics Workspace you created 

  <p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20210452.png"></p>

  • In Defender plan turn on the “Foundational CSPM” and “Servers” and click on “Save” button on top left

  <p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20210601.png"></p>

  • In Data collection select “All Events” and click on “Save” button on top left

  <p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20210755.png"></p>

  • Now move to next Task 

<br>

## Connecting Log Analytics Workspace to Virtual Machine 

  • Again, search for the “Log Analytics Workspaces” in the search bar of Azure 

  • Select the Log Analytics Workspace you created 

  • From left menu panel select “Virtual machines (deprecated)” in Classic section 

  • Select and open your Windows VM 
  
  <p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20211058.png"></p>

  • You can see that it is not connected with your Log Analytics Workspace, so now click on “Connect”

  <p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20211109.png"></p>

  • Let the process run and we can move to next task 

<br>

## Microsoft Azure Sentinel 

  • Now search for the “Microsoft Sentinel” in the search bar of Azure 

  • Now select “Create Microsoft Sentinel” 

  <p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20211403.png"></p>

  • Select the Log Analytics Workspace that you created so we can connect it with Microsoft Sentinel 

  <p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20211425.png"></p>

  • Now let's go to next task 

<br>

## Login to your Virtual Machine 

  1) Search for Virtual machine in Azure search Bar

        • Open the VM you created and copy the Public IP address so you can use it to 
          login from your own PC using “Remote Desktop Connection” application

     <p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20211551.png"></p>

  2) Open the “Remote Desktop Connection” on your own Windows PC. 

        • Paste your Public IP address then click on connect

     <p align="left"><img width="500" height="350" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20211741.png"></p> 

        • Now provide username and password that you created in our first task 

  3) Open the Event Viewer 

        • If you want to check logs of your login activity you can check it in Event viewer 

        • After opening the Event Viewer select the “Windows logs” and then “Security” 

        • Now you can see all the logs 

        • But our main focus will be event Id 4625, which signifies a failed login attempt.

     <p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20212557.png"></p>

        • Right now, you won’t see much action happening activity related to this event Id because we were able to successfully login to the system. But when you expose this VM to the open internet, everyone will try to brute force this VM. That’s what we want for this project so we can map the attack to get visualization. 

  4) First open Command prompt from your own computer to check if your VM is open to the internet. 

        • Use this command “ping [vm ip address] -t”  

        • If you see “Request timed out” message then you have to change the firewall rules in your VM windows machine

     <p align="left"><img width="600" height="300" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20213303.png"></p>

  5) Search for “wf.msc” in search bar to open the Windows Firewall 

        • Now Select “Windows Defender Firewall Properties”

     <p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20213448.png"></p>

        • Then turn off “Firewall state” in all sections. Turn off from “Domain Profile”, “Private Profile” and “Public Profile” 

        • Then click “Apply”

     <p align="left"><img width="500" height="300" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20213908.png"></p>

        • The purpose of this is to get as more hits as possible from all over the world

<br>

## Geo location API 

  • For this project we are going to use https://ipgeolocation.io/ , this allows us 1000 API request for free, which is enough for the purpose of this project 

  • Open the website click on sign up 

  • Create new account using your email or use your google account to sign in 

  • After sign in go to “Dashboard” 

  • You will find “API Key”, copy and save it you will need it for in the next task 

<p align="left"><img width="600" height="350" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20214615.png"></p>

<br>

## PowerShell Script 

  • We will use custom PowerShell script to get geo location of the IP addresses found in the Event Viewer with failed login attempt. 

  • Search for the “PowerShell ISE” in search bar of your connected Windows Virtual Machine and select “Run as administrator” 

  <p align="left"><img width="500" height="350" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20215044.png"></p>

  • Click on “New Script” button located under file option 

  • Copy and paste this custom script. [Click here](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Visual_Log_Exporter.ps1) 

  • Change the value of “$API_KEY” from the script to your own API key which you got from https://ipgeolocation.io/ website. (Note: My API key won’t work because I will delete it after finishing the project) 

<p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20215237.png"></p>

  • Now run the script. You will right away see the output of the sample log that we have setup in the script. If someone tries to brute force the VM, then you will see the new data right away. But sometime it may take some time so be patient. 

<p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20221859.png"></p>

  • This script will create “C:\ProgramData\failed_rdp.log” file. Copy the output from the file and save it in the file with the name “failed_rdp.log” in your own computer desktop 

  • You need to save this data in your own computer, so we can perform the next task 

<br>

## Creating Custom Log 

  • Search for the “Log Analytics Workspaces” in the search bar of Azure 

  • Select the Log Analytics Workspace you created 

  • Now select the “Tables” from Settings section 

  • Then click on “Create” and select “New custom log (MMA-based)” 

<p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20222726.png"></p>

  • Now you have to select and upload that “failed_rdp.log” file that you created in your own computer 

<p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20223052.png"></p>

  • Click next and go to “Collection paths”. Here select “Windows” from the dropdown under the Type section and in Path sections you can copy and paste this path “C:\ProgramData\failed_rdp.log” 

<p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20223514.png"></p>

  • Click next and give name to your log. You will need this name when you want to query the data 

<p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20223743.png"></p>

  • Now “Review + Create” 

  

   • If you want to test the query, go back to “Logs” and you will use your Custom log name to query the data. NOTE: It might take some time to get the log from your Windows Virtual Machine to Log Analytics Workspace 

<p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-25%20224023.png"></p>
<p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-26%20000106.png"></p>

  • To separate the Raw data in to custom field you can use this Custom query. [Click here](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Custom%20query.txt) 

<br>

## Set up Map in Sentinel 

  1) Create Workbook 

        • To create Workbook, open the Microsoft Sentinel 

        • Then select the Log Analytics Workspace that you created for this project. 

        • Then select “Workbook” located in Threat management section 

        • Select “Add Workbook”

        <p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-26%20001502.png"></p>

        • Here select “Edit” from top left and delete the default widgets provided by Azure by selecting “...” button on right side of the widgets 
        
        <p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-26%20001524.png"></p>

        • Now to add our own query you can select “Add” button from bottom left of the page, then select “Add query” 

        <p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-26%20001556.png"></p>

        • Now copy and paste this custom query to it. [Click here](https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Custom%20query.txt) 

        • Select “Map” from the drop-down of the Visualization. 

        <p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-26%20002022.png"></p>

        • Now “Run Query” and check if data is available 

          1) New section will appear on the right side 

          2) Here select “label” in Metric Label under the Metric Setting 

          3) Also change Metric Value to “event_count” located right under the Metric label 

          4) Hit “Apply” 

       <p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-26%20002546.png"></p>

        • Now to save this workbook, click on “Save” button located on top left of the page.  

        • You can give any name you like to save the workbook. Select your project resource in Resource group section. Also select the same region in Location section. Then hit “Apply”

        <p align="left"><img width="1000" height="500" src="https://github.com/mitesh72925/Using-Azure-Sentinel-to-Map-Live-Cyber-Attacks/blob/main/Images/Screenshot%202024-08-26%20002950.png"></p>

<br>

## How to Improve the security  

  1) Keep services and ports open that you need. Close all unnecessary ports and services. 

  2) Use secure services. Example: SSH instead of Telnet. HTTPS instead of HTTP.  

  3) Avoid using default Passwords and Username because when someone will try to do brute force, these credentials will be used first because its east to guess. 

  4) Use strong Password. You can use password managers to create and store your passwords. 

  5) One of the best practices is using Multi Factor Authentication.

<br>

## Reference and Appreciation 
  ### Special thanks to [Josh Madakor](https://www.youtube.com/@JoshMadakor), for providing idea for this project.   
