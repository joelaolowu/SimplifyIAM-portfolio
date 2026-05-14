# SimplifyIAM-portfolio
https://github.com/joelaolowu/SimplifyIAM-portfolio.git

www.linkedin.com/in/joelaolowu

#PROJECT PROBLEM: 

Simplifytech Service Company is a start up Comoany with over 200 staffs. It has a manual identity issue. The HR Department updates spread sheets as Staff lists. IT manually creates accounts one by one. Nobody knows who has access to what......


#MY JOB : 

To design and build their identity infrastructure MVP from scratch over five weeks and report to CISO. 

#TASK 1: 

I met with the IAM stakeholders for requirement gathering. AS an IAM person, to achieve th Requirements gathering, I had to speak five different Languages and not just Technical. The Languages are Data, Risk, Entitlements, Decision making and Company's Bottom line. The Stake holders i met with in the first week stakeholders workshop after i did the Stakeholhers Map were:


The HR TEAM: i did because HR owns the identity source and it's the quality and autentic data source


IT SECURITY: The CISO and the IT security head were in attendance. We discussed the entire program and it's governance. The policies relating to Controls etc.We discussed the risk reduction. 


APPLICATION OWNERS: We met to discuss the requirements and role mappings because without them, no role model exists, we discussed the connectors and how quick and best to connect without disturbing services, the SLA and Entitlement controls


THE AUDITORS: They will require evidence especially for control and Audit. 


BUSINESS MANAGERS: They approve or revoke access during certifications, They make Access decisions and Campaigns. 


THE IAM TEAM: I alongside my team mates represented the IAM team. We  were the implementers. 















Based on Requirements gathered from the workshops after series of arguements and deliberations with the Stakeholders, we decided to go with the following: For...

1.  HR

We deliberated on Workday, SAP and Successfactor for the HRM platform . For my MVP private environment the CSV connectors was used due to it's easy availability, costs and it works like it's done in most HR systems for convenience.



2.  IGA

The Stakeholders decided to pick an Identity Governance Administration platform using Sailpoint, Midpoint and Saviynt. The Midpoint was used as IGA by me for the desigm and building of the MVP due to costs, availability and the ease of connection to the connectors.The midpoint also works like Sailpoint and Savinyt.  



3.  Target Systems

The Active Directory, LDAP, Cloud Apps(Auth0) were decised after a series of deliberations by stake holders. I used the open LDAP for the ease of getting it and the cost of maintenance for my Lab environment and because it operates in the same was as the AD, LDAP and the Cloud and other SAAS Applications. 



4.  Access Management

OKTA, PING and Entra ID were deliberated at the Stakeholders workshop due to acceptance and efficiency in the Market, the End user Experience and the ease of Operations. For my Lab environment to demostrate these i used the Open LDAP because of the same way and ease of operations.



5.  Log Analysis

Sailpoint and Midpoint decided here for convenience and real time capabilities by the Auditors. The Midpoint is used for my MVP private Lab because of it's possibility of connecting easily to the Terminals and the Command lines. 























MY PRIVATE LAB ENVIRONMENT: 

This LAB is running till date. Please visit the server sites as links will be provided below. 



My private Lab Environment Details:

Server: simplifyiam-Joel-Adekunle-001

IP Address: 178.104.232.13







The three components in my lab:

SimplifyIAM (midPoint) is my IGA platform. This is where you configure provisioning rules, run reconciliation tasks, and manage identities. Access it at:

http://<your-ip>:8080/midpoint
Username: administrator
Password: @Admin123

SimplifyHR is my simulated HR system. This is my authoritative source of employees. When you add or terminate someone here, SimplifyIAM detects the change. Access it at:

http://<your-ip>:8085
No login required

phpLDAPadmin is my LDAP directory browser. This is where you see the target system -- accounts being created, modified, and disabled automatically. Access it at:

http://<your-ip>:8089
Bind DN: cn=Directory Manager
Password: Admin1234!



Accessing my Lab Server

SSH Access

SSH is built into both Windows and Mac. No additional software needed.

Windows — open PowerShell or Command Prompt:

ssh labuser@<your-ip>

Mac — open Terminal:

ssh labuser@<your-ip>

password is for labuser: simplifyiam

On first login you will be prompted to accept the server's fingerprint — type yes and press Enter.



Checking Service Status

Run these after login to confirm everything is running:

bash

# Status of all SimplifyIAM components
sudo /opt/simplifyiam/status-lab.sh

# SimplifyIAM (midPoint)
systemctl status midpoint

# SimplifyHR (the HR app)
systemctl status simplifyhr

# 389 Directory Server (LDAP)
systemctl status dirsrv@ldap1

A healthy service shows Active: active (running) in green.



Log Files

Use these to see what each service is doing in real time:

bash

# SimplifyIAM — tail the log live
sudo tail -f /opt/midpoint/midpoint-4.10/var/log/midpoint.log

# SimplifyHR — live log via journald
sudo journalctl -u simplifyhr -f

# 389 Directory Server — access log
sudo tail -f /var/log/dirsrv/slapd-ldap1/access

Press Ctrl + C to stop following a log.



Starting and Stopping Services

SimplifyHR and 389 DS start automatically on boot. SimplifyIAM requires a manual start after a reboot.

bash

# Start SimplifyIAM components
sudo /opt/simplifyiam/start-lab.sh

# Stop SimplifyIAM components
sudo /opt/simplifyiam/stop-lab.sh

[EXTRA COMMANDS BELOW - FOR REFERENCE ONLY]

# Stop a single service (replace midpoint with simplifyhr or dirsrv@ldap1)
sudo systemctl stop midpoint

# Restart a service
sudo systemctl restart midpoint




As an IAM person, i speak five different compulsory bu
