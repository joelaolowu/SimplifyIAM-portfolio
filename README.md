# SimplifyIAM-portfolio at https://github.com/joelaolowu/SimplifyIAM-portfolio.git

Hello all, My name is Joel A. Olowu an IAM Engineer with three years Experience in IGA, CIAM, Access Management and lately PAM. my linkedin profile can be viewed at www.linkedin.com/in/joelaolowu









#PROJECT:::


Simplifytech Service Company is a start up Company with over 200 staffs. It has a foundational problem. It has a manual identity issue. The HR Department updates spread sheets as Staff lists. It manually creates accounts one by one. Nobody knows who has access to what......


#MY JOB::: 


To design and build their identity infrastructure Minimum Viable Product where there would be birthright provisioning for users from scratch over five weeks and report to CISO. 









#TASK 1::: 



I met with the IAM stakeholders for requirement gathering. AS an IAM person, to achieve the Requirements gathering, I had to speak five different Languages and not just Technical. The Languages are Data, Risk, Entitlements, Decision making and evidence while keeping in mind the Company's Bottom line. We had to gather requirements from CISO/IT security discovery, HR workshops, Application workshops, Business workshops and Audit workshop. The Stake holders we met with in the first week stakeholders workshops after i did the Stakeholhers Map were:


The HR TEAM: i did because HR owns the identity source and it's the quality and autentic data source


IT SECURITY: The CISO and the IT security head were in attendance. We discussed the entire program and it's governance. The policies relating to Controls etc.We discussed the risk reduction. 


APPLICATION OWNERS: We met to discuss the requirements and role mappings because without them, no role model exists, we discussed the connectors and how quick and best to connect without disturbing services, the SLA and Entitlement controls


THE AUDITORS: They will require evidence especially for control and Audit. 


BUSINESS MANAGERS: They approve or revoke access during certifications, They make Access decisions and Campaigns. 


THE IAM TEAM: I alongside my team mates represented the IAM team. We  were the implementers. 




:::WHAT SIMPLIFYTECH REALLY NEEDS THAT MADE ME DECIDE ON THE ARCHITECTURE::: 


:IDENTITY SOURCE:

The HR spreadsheet needs a system of records that IGA can read automatically. No manual export. 


:THE TARGET SYSTEMS: 

AD equivalent for all staff accounts. Every employee needs. directory account on day 1. 


:LIFECYCLE AUTOMATION: 

Joiner, mover an leaver mut be triggered by HR events. No IT tickets. Zero manual provisioning. 


:AUDIT TRAIL:

SOC2 requires evidence of who had access ? When it was granted ? when it was removed ? and who approved it ? 




















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




























































:::MY PRIVATE LAB ENVIRONMENT:::


This LAB is running till date. Please visit the server sites as links will be provided below. 



My private Lab Environment Details:

Server: simplifyiam-Joel-Adekunle-001









The three components in my lab:


SimplifyIAM (midPoint) is my IGA platform. It is similar to sailpoint. This is where you configure provisioning rules, run reconciliation tasks, and manage identities. Access it at:


http://[SERVER IP]/midpoint



SimplifyHR is my simulated HR system. This is my authoritative source of employees. When you add, move or terminate someone here, SimplifyIAM detects the change. I demonstration to prove these is done below.

http://[SERVER IP]:8085
No login required


phpLDAPadmin is my LDAP directory browser. This is where you see the target system -- accounts being created, modified, and disabled automatically. Access it at:

http://[SERVER IP]:8089
Bind DN: cn=Directory Manager




I Access my Lab Server through SSH Access

SSH is built into both Windows and Mac. No additional software needed for SSH.

for Windows — open PowerShell or Command Prompt:

ssh labuser@[SERVER IP]
password is [SSH PASSWORD] .





for Mac — open Terminal:

ssh labuser@[SERVER IP]

password for labuser: [SSH PASSWORD]

On first login i am prompted to accept the server's fingerprint —so i type yes and press Enter.



For Checking Service Status on the IGA, Connected makeshift HR platform and LDAP,

I run these bash commands after login to confirm everything is running:



# Status of all SimplifyIAM components
sudo /opt/simplifyiam/status-lab.sh

# SimplifyIAM (midPoint)
systemctl status midpoint

# SimplifyHR (the HR app)
systemctl status simplifyhr

# 389 Directory Server (LDAP)
systemctl status dirsrv@ldap1

A healthy service shows Active: active (running) in green as below

! [image Alt](https://github.com/joelaolowu/SimplifyIAM-portfolio/blob/e73e90b2699ed4849a43a14347209febd06513bc/checking%20to%20confirm%20services%20.png)

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













































Phase 1 Summary

•       SimplifyHR CSV resource created and connected
•       Seven inbound mappings configured and saved
•       Three synchronization reactions configured
•       Correlation rule set - Item=name, Exact match
•       Reconciliation ran - six focus objects created in midPoint
•       Data preview shows all six employees as LINKED

Phase 2
•       OpenLDAP created as a target resource in midPoint
•       Object type configured - inetOrgPerson with nsAccount auxiliary class
•       Seven outbound mappings configured including CN and DN scripts
•       Synchronization reactions configured on OpenLDAP resource
•       Correlation rule configured to link LDAP accounts to focus objects
•       Employee role updated with OpenLDAP construction - the missing link
•       Object Template configured - Employee role assigned automatically to all users
•       SimplifyHR reconciliation re-run - six accounts appear in ou=people in OpenLDAP
•       Leaver workflow - Oliver Bennett terminated, account moves to ou=inactive
















What i Built...

SimplifyHR connected to midPoint as a CSV source resource
Six employee identities created automatically in midPoint via reconciliation
OpenLDAP connected as a target resource with full outbound mappings including CN and DN scripts
Six LDAP accounts provisioned automatically to ou=people - full attribute set including costcenter
Live joiner demonstrated - John Wick added in SimplifyHR, reconciliation run, account appeared in ou=people automatically with zero manual steps
Leaver process - Oliver Bennett terminated in SimplifyHR, LDAP account removed from ou=people automatically on next reconciliation run
Full audit trail in midPoint - every identity event logged with timestamp and initiator










:::TASK 2:::


Creating the SimplifyHR Resource

 
Go to midPoint → Resources → All resources → click New resource. 
Click From Scratch. Then click CsvConnector (com.evolveum.polygon.connector.csv.CsvConnector v2.9).
 
Step 1a - Basic Information
1.     Name: SimplifyHR
2.     Description: HR resource to map users from source to IGA (midpoint)
3.     Lifecycle state: change from Proposed (simulation) to Active (production)
4.     Click Next: Configuration →
 
Step 1b - Configuration
5.     File path: /opt/midpoint/var/hr.csv
6.     Click Next: Discovery →
 
Step 1c - Discovery
midPoint reads the CSV and detects the structure. 
Delete value in multi-valued attribute

Configure Name attribute = empid and Unique attribute name = empid. Do not change anything.
7.     Click Next: Schema →
 
Step 1d - Schema
Account ObjectClass is shown with type Structured. Check the checkbox - it should already be selected.
8.     Click Create resource

Step 1e - Disable Delete Capability on SimplifyHR
SimplifyHR is your source of truth. midPoint should never delete records from the CSV. The Delete capability is enabled by default - disable it now for security reasons.
On the SimplifyHR resource page scroll down to List of capabilities.
You will see Delete with a green filled circle - that means it is enabled.

To disable it:

-Click directly on the Delete capability icon
-It will toggle to grey/disabled state
-Click Save (top left)

Why this matters: Without disabling Delete, if you accidentally delete a identity object in midPoint, midPoint will also remove the employee row from hr.csv. SimplifyHR is the system of record - midPoint only reads from it, never writes to it.








2. Configuring the Object Type

 
On the SimplifyHR resource, click Schema handling in the left menu. Click the object type to configure it. You will see the Object type wizard with 7 sections. 
Step 2a - Basic information about the object type
9.     Display name: Account
10.  Kind: Account
11.  Lifecycle state: Active (production)
12.  Click Next: Resource data →


Step 2b - Resource data

13.  Object class: AccountObjectClass  (already selected)
14.  Click Next: MidPoint data →
    
Step 2c - MidPoint data

16.  Type: User  (already selected)
17.  Archetype: No archetype  (already selected)
18.  Click Save settings




3 Configuring Inbound Mappings

 
From the Object type wizard, click Mappings. Make sure you are on the Inbound mappings (to MidPoint) tab.
 
Add each mapping by clicking Add inbound. Your completed table will match the screenshot above.
 
Mapping 1 - EmpID → name

18.  Name: EmpID
19.  From resource attribute: empid
20.  Expression: As is
21.  Target: name
22.  Lifecycle state: Active (production)
 
     mapping 2 - EmpID → emailAddress  (Groovy script)

23.  Name: Email
  
24.  From resource attribute: empid
25.  Expression: Script → click Show script
26.  Language: Groovy (default)
27.  Code - paste exactly:
 
input + '@simplifytech.com'

 
28.  Click Done
29.  Target: emailAddress
30.  Lifecycle state: Active (production)
  
✅  Verify: empid → Script (Evaluator value is set) → emailAddress

 
Mapping 3 - firstname → givenName
31.  Name: FirstName  |  From: firstname  |  Expression: As is  |  Target: givenName
✅  Verify: firstname → As is → givenName

 
Mapping 4 - lastname → familyName
32.  Name: LastName  |  From: lastname  |  Expression: As is  |  Target: familyName
✅  Verify: lastname → As is → familyName

 
Mapping 5 - department → organizationalUnit
33.  Name: Department  |  From: department  |  Expression: As is  |  Target: organizationalUnit
✅  Verify: department → As is → organizationalUnit

 
Mapping 6 - costcenter → costCenter
34.  Name: costcenter  |  From: costcenter  |  Expression: As is  |  Target: costCenter
✅  Verify: costcenter → As is → costCenter

 
Mapping 7 - status → activation/administrativeStatus  (Groovy script)
35.  Name: Status
36.  From resource attribute: status
37.  Expression: Script → click Show script
38.  Language: Groovy (default)
39.  Code - paste exactly:
 

Write groovy script below:

import com.evolveum.midpoint.xml.ns._public.common.common_3.ActivationStatusType if (input == 'Active') {     return ActivationStatusType.ENABLED } else {     return ActivationStatusType.DISABLED }





40.  Click Done
41.  Target: activation/administrativeStatus
42.  Lifecycle state: Active (production)
 
✅  Verify: status → Script (Evaluator value is set) → activation/administrativeStatus

 
Click Save mappings.
✅  Verify: All 7 mappings saved. Mappings screen matches the screenshot on page 7.









:::4, Configure Synchronization Reactions:::

 
From the Object type wizard, click Synchronization.
  
Add these three reactions - click Add reaction for each:
 
Situation-Action-Linked-Synchronize

Unlinked-Link

Unmatched-Add focus

 
***Pls note, don't ever add or Do NOT add a Deleted reaction***. Without it, midPoint will not touch the CSV file if a focus object is deleted in midPoint.

 
Click Save synchronization settings.
✅  Verify: Three reactions saved.

 
5, Configure the Correlation Rule

 
From the Object type wizard, click Correlation.

Click on the account correlation rule to edit it.
 
The correlator is set to Item=name with Exact match.

his is correct: leave it as is. Click Save 2 times

name in midPoint holds the empid value from the CSV. Exact match on name prevents duplicate identities.

43.  Click Confirm settings
44.  Click Save correlation settings
✅  Verify: Correlation rule saved with Item=name, Exact match.

 
6, Run the Reconciliation Task

 
Go to Server tasks → All tasks → find your reconciliation task, or create a new one:
New task → Reconciliation → Resource: SimplifyHR → Kind: Account → Intent: default → Object class: AccountObjectClass
  
45.  Click Save & Run  (or Run now)
Wait for the task to show 100.0% (closed).
✅  Verify: Task completes showing 100.0% (closed) with a start and end timestamp.

 Note: The task result might show an error, ignore it. This occurs because of reference in role object, which gets resolved once the OpenLDAP resource is created (in Phase 2 later).

 
7, Verify - Data Preview and Users Page

 
Check Data Preview
Go to SimplifyHR resource → Schema handling → Account object type → click Preview data.
  
✅  Verify: Six rows. All show LINKED. Owner column shows empid. Phase 1 is complete.

 
Check midPoint Users page
Go to Administration → Users. Six users should appear - 1001 through 1006.
•       Click any user - confirm givenName, familyName, emailAddress, costCenter are populated
•       emailAddress format: 1001@simplifytech.com  (empid + domain)

phpLDAPadmin will still show an empty directory. That is correct.
Phase 1 creates identities in midPoint only.
Phase 2 will provision those identities to OpenLDAP.


7, Check Audit Log


Go to Reports → Audit Log Viewer in midPoint.
Filter by: Event Type → Object Add
Filter by: Timestamp - today's date
Take a screenshot of the audit logs
This is your evidence that midPoint created the identities automatically - not a human, not a script.

✅  Verify: Audit log shows Object Add entries with timestamps matching your reconciliation run.


Phase 1 Complete Summary:

•       SimplifyHR CSV resource created and connected




















PHASE 2,












1, Create the OpenLDAP Resource

 
Go to midPoint → Resources → All resources → click New resource.
 
Click From Scratch. In the Resource catalog click LdapConnector - com.evolveum.polygon.connector.ldap.LdapConnector v3.9.2
 
Step 1a - Basic Information
1.     Name: OpenLDAP
2.     Description: A target application that requires accounts to be provisioned (or removed) depending on user status in IGA.
3.     Lifecycle state: Active (production)
4.     Click Next: Configuration →
  
Step 1b - Configuration (Establish a connection)
5.     Host: localhost
6.     Port number: 389
7.     Connection security: leave blank
8.     Bind DN: cn=Directory Manager
9.     Bind password: Use clear value - enter your LDAP admin password (see Skool Pro Module 0 Credentials lesson)

10.  Click Next: Discovery →
  
If the connection fails here - check that 389 Directory Server is running: SSH into your server and run: sudo systemctl status dirsrv@ldap1

 
Step 1c - Discovery

midPoint connects to 389 DS and detects the base context automatically.
11.  Base context: dc=simplifyiam,dc=com  (auto-detected)
12.  Do not change anything
13.  Click Next: Schema →
  
Step 1d - Schema

midPoint reads the LDAP schema. You need to select three object classes:
14.  Check account (native name: account) - this is the primary structural class
15.  Also select inetOrgPerson and nsAccount from the list - these are the object classes used by 389 DS
To find inetOrgPerson and nsAccount - use the Search box or scroll through the list. Check both.
 
16.  Click Create resource
 
✅  Verify: Resource OpenLDAP has been created page appears with four options: Preview Resource Data, Configure Object Types, Configure Association Types, Go To Resource

 
 
2, Configure the Object Type on OpenLDAP

 
From the confirmation screen click Configure Object Types. Or go to OpenLDAP resource → Schema handling → Object types → Add object type.
  
Step 2a - Basic information about the object type
17.  Display name: Account
18.  Kind: Account
19.  Intent: default
20.  Lifecycle state: Active (production)
21.  Click Next: Resource data →
  
Step 2b - Resource data
22.  Object class: inetOrgPerson  (select from dropdown)
23.  Auxiliary object class: nsAccount  (click Add value and select nsAccount)
24.  Click Next: MidPoint data →

Step 2c - MidPoint data

25.  Type: User  (already selected)
26.  Archetype: No archetype  (already selected)
27.  Click Save settings
  
✅  Verify: Object type saved. Object type wizard appears with 8 sections: Basic Attributes, Mappings, Synchronization, Correlation, Capabilities, Activation, Credentials, Policies

3, Configure Outbound Mappings

 
From the Object type wizard click Mappings. Click the Outbound mappings (to Resource) tab.
You will configure seven outbound mappings. These define which midPoint focus object attributes get written to LDAP when an account is provisioned.
  
Your completed outbound mappings table will look like this: 

Mapping 1 - givenName → givenName

28.  Name: firstname
29.  Source: givenName  (from focus object)
30.  Expression: As is
31.  To resource attribute: givenName
32.  Lifecycle state: Active (production)
✅  Verify: givenName → As is → givenName

 
Mapping 2 - familyName → sn

33.  Name: lastname
34.  Source: familyName
35.  Expression: As is
36.  To resource attribute: sn
37.  Lifecycle state: Active (production)
✅  Verify: familyName → As is → sn

 
Mapping 3 - cn  (Groovy script - full name)

38.  Name: cn
39.  Source: familyName AND givenName  (add both as sources)
40.  Expression: Script → click Show script
41.  Language: Groovy (default)
42.  Code - paste exactly:
    
 givenName + ' ' + familyName

 
44.  Click Done
45.  To resource attribute: cn
46.  Lifecycle state: Active (production)
 
✅  Verify: cn row shows familyName + givenName sources, Script expression with tooltip givenName + ' ' + familyName

 
Mapping 4 - DN  (Groovy script - routes Active to ou=people, Terminated to ou=inactive)

46.  Name: DN
47.  Source: name  (from focus object)
48.  Expression: Script → click Show script
49.  Language: Groovy (default)
50.  Code - paste exactly:
 
import com.evolveum.midpoint.xml.ns._public.common.common_3.ActivationStatusType

if (user?.activation?.administrativeStatus == ActivationStatusType.DISABLED) 
{ 	
return 'uid=' + name + ',ou=inactive,dc=simplifyiam,dc=com' 
} 
else 
{ 	
return 'uid=' + name + ',ou=people,dc=simplifyiam,dc=com' 
}

 
51.  Click Done
52.  To resource attribute: dn
53.  Lifecycle state: Active (production)
 
✅  Verify: DN row shows name source, Script expression - Evaluator value is set
This script is the Leaver logic. When Oliver Bennett is terminated (status = Disabled), his account DN is routed to ou=inactive instead of ou=people. The account moves - it is not deleted.

 
Mapping 5 - emailAddress → mail

54.  Name: emailAddress
55.  Source: emailAddress
56.  Expression: As is
57.  To resource attribute: mail
58.  Lifecycle state: Active (production)


Mapping 6 - costCenter → departmentNumber

59.  Name: costCenter
60.  Source: costCenter
61.  Expression: As is
62.  To resource attribute: departmentNumber
63.  Lifecycle state: Active (production)
✅  Verify: costCenter → As is → departmentNumber

 
Mapping 7 - name → employeeNumber

64.  Name: name
65.  Source: employeeNumber  (from focus object)
66.  Expression: As is
67.  To resource attribute: employeeNumber
68.  Lifecycle state: Active (production)
✅  Verify: employeeNumber → As is → employeeNumber

 
Click Save mappings.
✅  Verify: All 7 outbound mappings saved. Table matches the screenshot above.

 
 
4, Configure Synchronization Reactions on OpenLDAP

 
From the Object type wizard click Synchronization. These reactions define what midPoint does when it finds accounts during LDAP reconciliation.
  

::Add these three reactions::


Situation-Action-Linked-Synchronize
Unlinked-Link
Unmatched-Add focus

 
Click Save synchronization settings.
✅  Verify: Three reactions saved.

5, Configure Correlation Rule on OpenLDAP

 
From the Object type wizard click Correlation. This tells midPoint how to match existing LDAP accounts to focus objects.
  
69.  Add a correlation rule - name it: account correlation
70.  Description: Correlation - to link identity to account in LDAP
71.  Click ticket box on the right on the rule to configure the correlator
72.  Correlator item: name  (this matches the uid in LDAP against the focus object name)
73.  Search method: Exact match
74.  Click Confirm settings
75.  Click Save correlation settings
✅  Verify: Correlation rule saved - account correlation - Enabled=True

 
 
6, Add Employee Role Construction - The Missing Link

 
The Employee role needs an inducement that points to the OpenLDAP resource. When a user is assigned the Employee role, midPoint automatically creates their LDAP account.
 
Why this is needed: midPoint does not provision accounts to LDAP just because a resource exists.
You need to tell midPoint: for every user with the Employee role, create an account in OpenLDAP.
That instruction lives in the role of an inducement with a construction block.

 

Add the construction to the Employee role

76.  Go to Roles → Employee
77.  Click the Inducements tab. Delete existing any inducements that might be there and pointing to non-existing resources.
78.  Click Add inducement → Construction
79.  Resource: select OpenLDAP from the dropdown (the current resource - not the old one)
80.  Kind: Account
81.  Intent: default
82.  Click Save
  
✅  Verify: Employee role Inducements tab shows: OpenLDAP - Kind: ACCOUNT - Intent: default


:::I ran simplyfyHR reconciliation task to provision accounts to LDAP:::


Now run the SimplifyHR reconciliation task again. This time, because the Employee role is automatically assigned and the role has an OpenLDAP construction, accounts will be provisioned to LDAP automatically.
  
93.  Go to Server tasks → All tasks
94.  Find: Reconciliation task: SimplifyHR: Account
95.  Click Run now
  
While the task runs - switch to phpLDAPadmin and click Refresh. Watch accounts appear under ou=people.
 
✅  Verify: Task completes 100%. Six accounts appear in phpLDAPadmin under ou=people.

 
Verify in midPoint OpenLDAP Accounts tab
Go to Resources → OpenLDAP → Accounts tab.
  
✅  Verify: Six accounts listed - uid=1001,ou=people through uid=1006,ou=people - all showing situation LINKED

 
Verify in phpLDAPadmin
 
✅  Verify: phpLDAPadmin shows six accounts under ou=people. ou=inactive exists and is empty - it will receive terminated accounts.


:::WHAT I BUILT:::


•       OpenLDAP resource created with LdapConnector
•       Object type configured: inetOrgPerson with nsAccount auxiliary class
•       Seven outbound mappings: givenName, sn, cn (script), DN (script), mail, departmentNumber, employeeNumber
•       DN script routes active users to ou=people and terminated users to ou=inactive
•       Synchronization reactions and correlation rule configured on OpenLDAP resource
•       Employee role updated with OpenLDAP construction inducement
•       Six accounts provisioned to ou=people automatically via reconciliation












::: THE JOINER PROCESS  :::



Joiner Process
New employee provisioned automatically - SimplifyHR → midPoint → OpenLDAP

 
1, Add New Employee in SimplifyHR

 
Go to SimplifyHR at http://[your-ip]:8085
Click the + Provision Employee button (top right).
  
Fill in the form:
1.     First Name: John
2.     Last Name: Wick
3.     Organizational Department: Operations
The Pipeline Payload Preview shows exactly what will be written to hr.csv - empid auto-assigned as 1007, costcenter auto-generated as OPS-auto.
4.     Click Commit Record
 
✅  Verify: SimplifyHR now shows Total Workforce=7, Active Identities=7, John Wick appears as empid 1007 in the list

 
2, Run SimplifyHR Reconciliation Task

 
Go to midPoint → Server tasks → All tasks.
Find: Reconciliation task: SimplifyHR: Account
5.     Click Run now
Wait for the task to complete - watch the status indicator turn green.
  
This single task triggers the entire Joiner pipeline:

1. midPoint reads the CSV and detects John Wick as a new Unmatched record
2. A new focus object is created for John Wick
3. The Employee Template fires - Employee role is assigned automatically
4. The Employee role construction triggers - midPoint creates John Wick's LDAP account in ou=people

All of this happens in one reconciliation run with zero manual steps.

 
3, Verify in midPoint Users Page

Go to Administration → Users.

John Wick now appears as user 1007 with email 1007@simplifytech.com.
  
Accounts column shows 2 for John Wick - one account in SimplifyHR resource (shadow), one account in OpenLDAP. This confirms end-to-end provisioning worked.






4, Verify in phpLDAPadmin

 
Open phpLDAPadmin at http://[your-ip]:8089
Navigate to ou=people - you should now see seven entries: uid=1001 through uid=1007.
  
✅  Verify: uid=1007 (John Wick) appears under ou=people. Seven accounts total. ou=inactive is still empty.

 
Joiner process complete.


New employee added in SimplifyHR → reconciliation run → focus object created in midPoint → Employee role assigned automatically → LDAP account created in ou=people.
Zero manual steps after the initial SimplifyHR entry.


 

 


 
::: LEAVER PROCESS :::

Leaver Process

Employee terminated in HR - account automatically removed from OpenLDAP

 
5, Trigger Leaver Flow for Oliver Bennett in SimplifyHR

 
Oliver Bennett (empid 1006, Engineering, ENG-004) is being terminated.
In SimplifyHR, find Oliver Bennett in the Identity Records list.
6.     Click Trigger Leaver Flow next to Oliver Bennett
The button for Oliver Bennett becomes highlighted - confirming the action is about to fire.
  
6, Run SimplifyHR Reconciliation Task

 
Go to midPoint → Server tasks → All tasks.
7.     Click Run now on Reconciliation task: SimplifyHR: Account
Wait for task to complete.

After the task completes, check SimplifyHR:
 
✅  Verify: SimplifyHR: Oliver Bennett (1006) shows Terminated status. Active Identities=6, Terminated Records=1.

 
7, Verify Oliver Bennett Disabled in midPoint

 
Go to midPoint → Administration → Users.
User 1006 (Oliver Bennett) shows a disabled icon - the activation status tooltip says Activation Status: disabled.
  
Oliver Bennett's Accounts column now shows 1 - only the SimplifyHR shadow remains.
The OpenLDAP account has been deleted.

***Note: In this lab configuration the account is deleted from OpenLDAP on termination.
In a production environment you would configure the DN script to move the account to ou=inactive instead - see Phase 2 guide for the DN script configuration.

8, Verify Account Deleted in phpLDAPadmin

 
Open phpLDAPadmin and refresh the tree.

Navigate to ou=people - you should now see six entries.
  
✅  Verify: uid=1006 (Oliver Bennett) is no longer in ou=people. Six accounts remain: 1001-1005 and 1007 (John Wick).





Leaver process complete.

Oliver Bennett terminated in SimplifyHR → reconciliation run → Oliver Bennett disabled in midPoint → OpenLDAP account deleted.

Zero manual steps after the Trigger Leaver Flow action in SimplifyHR.

The full audit trail in the midPoint Records tab shows the complete lifecycle for Oliver Bennett: account created, provisioned, and removed - all timestamped.


Summary Event -Trigger-Result


Joiner-Provision Employee in SimplifyHR + run reconciliation
Focus object created, Employee role assigned, LDAP account created in ou=people

Leaver

Trigger Leaver Flow in SimplifyHR + run reconciliation
Focus object disabled in midPoint, LDAP account deleted from ou=people





:::What You Built:::......


-SimplifyHR connected to midPoint as a CSV source resource


-Six employee identities created automatically in midPoint via reconciliation

-OpenLDAP connected as a target resource with full outbound mappings including CN and DN scripts

-Six LDAP accounts provisioned automatically to ou=people - full attribute set including costcenter

-Live joiner demonstrated - John Wick added in SimplifyHR, reconciliation run, account appeared in ou=people automatically with zero manual steps

-Leaver process - Oliver Bennett terminated in SimplifyHR, LDAP account removed from ou=people automatically on next reconciliation run
Full audit trail in midPoint - every identity event logged with timestamp and initiator











