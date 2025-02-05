# Securing SMBv1/SMBv2/SMBv3 for Windows servers 
**Authored by Zachary Thill - IT Student Project Leader @ RRCC**


# What is SMB? # 
- SMB, or (Server Message Block protocol) is a network file sharing protocol that allows applications on a computer to read and write to files and to request services 
  from server programs in a computer network. Not only does SMB allow computers to share files, but it also enables computers to share printers and even serial ports 
  from other computers within the network.  
  
# History of SMB 
 - In 2017, the imfanous WannaCry Ransomware was a exploit for SMB version 1, infected hundreds of thousands of devices and encrypted their data. In order
   for companies to get their data back, they had to pay a ransom in Bitcoin.Originally created by the NSA for snooping, EternalBlue was the tool used to carryout this 
   attack that made the threat actors over 100,000 dollars in bitcoin at the time (Just imagine if they saved all that until now). As a server admin, make sure to 
   disable SMBv1 and SMBv2 as they are not the latest version. SMBv3 is the latest and most secure version of SMB and currently, there are no known vulnerabilities 
   reported or exploited.  
   
   **TO DEACTIVATE ALL SMB TRAFFIC FOR ULTAMITE SECURITY, MAKE A FIREWALL RULE DROPPING / DENYING PORTS 139 AND 445**
   
 # How to Secure SMB via Active Directory
   
 **Step 1** - Go to "Group Policy Managment" and continue to your Domain **->** "Group Polcy Objects" **->** Right Click Default Domain policy **->** Click "Edit" 
   
 **Step 2** - In "Computer Configuration" **->** "Preferences" **->** "Windows Settings" **->** "Registry", create a new rule(Once pushed out, this will send to all windows servers)

 **Step 3** - Right Click, then Click 'New" **->** "Registry Item" 
   
 **Step 4** - Change "Update' Action to "Create" and in Key Path, typ, "SYSTEM\CurrentControlSet\Services\Lanmanserver\Parameters" 
   
 **Step 5** - In Value Name, Type, "SMB1" and change Value Type to "REG_DWORD" and in Value data, put "0"
   
 **Step 6** - Click "OK"
   
 **Step 7** - To Disable SMBv1 from the local machine, repeat steps 4-6 exept keep Action as "Update" and Key path is "SYSTEM\CurrentControlSet\Services\mrxsmb10" 
            Set Valu name to "4" **->** Vlaue Type to "REG_DWORD" and Click "OK" 
   
 **Step 8** - Make another registry action **->** set Action to "Replace" **->** Key path "SYSTEM\CurrentControlSet\Services\LanmanWorkstation"
            Vlaue Name "DependOnService" **->** Value type "REG_MULTI_SZ" **->** Value data "Browser "
                                                                                    "MRxSmb20" 
                                                                                    "NSI     " Click "OK" 
 
 **YOU MUST REBOOT IN ORDER FOR THESE RULES TO TAKE EFFECT**
 

# Setup SMB Signing 
**(This Security Policy will make signatures for all SMB traffic and let any workstation/Server know if SMB traffic has been Intercepted / Manipulated)**

 **Step 1** - In "Default Domain Policy / Policies / Winsows Settings / Security Settings / Local Policies / Security Options" 

 **Step 2** - Double Click "Microsoft Network Client: Digitally sign communications [always]" **->** Click "Define this setting" **->** 'Enabled" **->** "Apply" 
                                                           
 **Step 3** - Do the exact same thing twice. There are 2 differnet security policies with the same name as above. One is Servers and the other in Clients.
                                                                                    
   # Force the New Group Policy out to all Networked Devices  
   
 **Step 1** - Go to "Group Policy Manager' **->** "Your Domain" **->** "Starter GPO's" 

 **Step 2** - 
