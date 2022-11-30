  

  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

  

* * *

[[_TOC_]]

* * *

Introduction
============

This runbook is part of an AWS Runbook series meant to provide the foundation for a customer’s AWS Operational Knowledge Base. This guide provides the descriptions and methods for deploying the AWS Discovery Service Connector. One common usage of the ADS Connector is to capture data needed for input into Application Portfolio Assessment activities that are part of the Migration Readiness and Planning phase of migrating to AWS. 

Using this Runbook
==================

Each customer environment is unique, so this runbook should be revised to include any existing customer specific processes. The runbooks in this series are also published in Word format but are more valuable when incorporated into a Knowledge Management System that supports linking and indexing.

Overview 

==========

The AWS Application Discovery Service helps you plan application migration projects by automatically identifying servers, virtual machines (VMs), software, and software dependencies running in your on-premises data centers. Application Discovery Service also collects application performance data, which can help you assess the outcome of your migration. The data collected by Application Discovery Service is securely retained in an AWS-hosted and managed database in the cloud. You can export the data as a CSV or XML file into your preferred visualization tool or cloud-migration solution to plan your migration. See the full AWS Application Discovery Service User Guide [here](https://docs.aws.amazon.com/application-discovery/latest/userguide/appdiscovery-ug.pdf).

Application Discovery Service offers two modes of operation: 

*   **Agentless discovery mode** is recommended for environments that use VMware vCenter This mode doesn't require you to install an agent on each host. Agentless discovery gathers server information regardless of the operating systems, which minimizes the time required for initial on-premises infrastructure assessment. Agentless discovery doesn't collect information about software and software dependencies. It also doesn't work in non-VMware environments.  
    

The agent-based discovery mode will not be used for the initial implementation. 

*   **Agent-based discovery mode** collects a richer set of data than agentless discovery by using Amazon software, the AWS Application Discovery Agent, which you install on one or more hosts in your data center. The agent captures infrastructure and application information, including an inventory of installed software applications, system and process performance, resource utilization, and network dependencies between workloads. The information collected by agents is secured at rest and in transit to the Application Discovery Service database in the cloud. Agent-based discovery works in both VMware and non-virtualized environments. 
    

We recommend that you use agent-based discovery for non-VMware environments and to collect information about software and software dependencies. You can also run agent-based and agentless discovery simultaneously. Use agentless discovery to quickly complete the initial infrastructure assessment and then install agents on select hosts. 

Required Information 
 
=======================

|   **Name**     |   **Value**     |
| --- | --- |
|   AWS Account where ADS is configured     |   Customer Shared Services Account - xxxxxxxxxxxx   |
|   ADS IAM User     |   {AWS-ServerMigrationService}  arn:aws:iam::xxxxxxxxxxxx:user/AWS-ApplicationDiscoveryService      |
|   Required ADS IAM Policies     |   AWSAgentlessDiscoveryService     |
|   ADS Connector Hostname     |         |
|   ADS Connector Static IP     |         |
|   ADS Connector OV File Download Link     |   Agentless Discovery Appliance [OVA](https://s3-us-west-2.amazonaws.com/aws.agentless.discovery.connector.bundle/latest/AWSDiscoveryConnector.ova) ([MD5](https://s3-us-west-2.amazonaws.com/aws.agentless.discovery.connector.bundle/latest/AWSDiscoveryConnector.ova.md5) and [SHA256](https://s3-us-west-2.amazonaws.com/aws.agentless.discovery.connector.bundle/latest/AWSDiscoveryConnector.ova.sha256) checksums for verification)   [https://s3-us-west-2.amazonaws.com/aws.agentless.discovery.connector.bundle/latest/AWSDiscoveryConnector.ova](https://s3-us-west-2.amazonaws.com/aws.agentless.discovery.connector.bundle/latest/AWSDiscoveryConnector.ova)   |
|   vCenter Service Account (AD Account)     |           |
|   vCenter Permissions     |     Read-only       |
|   Network Connectivity   |   *   ADS Connector requires port 443 access to the Internet     *   ec2.amazonaws.com     *   iam.amazonaws.com  *   *   arsenal.us-west-2.amazonaws.com     *   sms.us-west-2.amazonaws.com     *   s3.us-west-2.amazonaws.com     *   s3.us-west-1.amazonaws.com     *   sns.us-west-1.amazonaws.com     *   awsconnector.us-west-2.amazonaws.com     *   connector-platform-upgrade-info.s3-us-west-2.amazonaws.com     *   server-migration-service-upgrade.s3-us-west-2.amazonaws.com     *   prod.agentless.discovery.connector.upgrade.s3-us-west-2.amazonaws.com *   ADS Connector requires port 443 access to the vCenter host that it will collect data from.           |
| Management Endpoint Network Connectivity |   [https://ajax.googleapis.com/ajax/libs/jquery/1.12.0/jquery.min.js](https://ajax.googleapis.com/ajax/libs/jquery/1.12.0/jquery.min.js)  [https://netdna.bootstrapcdn.com/font-awesome/4.0.3/css/font-awesome.min.css](https://netdna.bootstrapcdn.com/font-awesome/4.0.3/css/font-awesome.min.css)  [https://code.jquery.com/ui/1.11.4/themes/smoothness/jquery-ui.css](https://code.jquery.com/ui/1.11.4/themes/smoothness/jquery-ui.css)  [https://code.jquery.com/jquery-1.10.2.js](https://code.jquery.com/jquery-1.10.2.js)  [https://code.jquery.com/ui/1.11.4/jquery-ui.js](https://code.jquery.com/ui/1.11.4/jquery-ui.js)   |

ADS Setup 

===========

This section describes the steps required to set up the Application Discovery Service. 

Request an internal hostname and static IP for the ADS connector 

------------------------------------------------------------------

The static IP assignment is optional, based on the customer's process for assigning server IP addresses.

Set up Agentless Discovery 

----------------------------

To set up agentless discovery, you must deploy the AWS Agentless Discovery Connector virtual appliance on a VMware vCenter Server host in your on-premises environment. After you deploy the virtual appliance, you must configure the connector using the web-based console. 

### Deploying the AWS Agentless Discovery Connector Virtual Appliance 

**To deploy the connector virtual appliance** 

1.  Sign in to vSphere client as a VMware administrator.
2.  Download the OVA file for the ADS Connector.
    1.  [https://s3-us-west-2.amazonaws.com/aws.agentless.discovery.connector.bundle/latest/AWSDiscoveryConnector.ova](https://s3-us-west-2.amazonaws.com/aws.agentless.discovery.connector.bundle/latest/AWSDiscoveryConnector.ova)
3.  Choose File, Deploy OVF Template.
4.  Choose Browse and select the OVA file that you downloaded.
5.  Change the name of the connector to the hostname listed in the table above.
6.  On the Disk Format page, select one of the thick provision disk types. We recommend that you choose **Thick Provision Eager Zeroed**, because it has the best performance and reliability. However, it requires several hours to zero out the disk. Do not choose Thin Provision. This option makes deployment faster but significantly reduces disk performance. For more information, see [Types of supported virtual disks](http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1022242)in the VMware documentation. 
    
7.  Locate and open the context (right-click) menu for the newly deployed template in the vSphere client inventory tree and choose Power, Power On. Open the context (right-click) menu for the template again and choose Open Console. The console displays the IP address of the connector console. Save the IP address in a secure location. You need it to complete the connector setup process.
8.  If the customer must assign a static IP to the ADS Connector:
    1.  Locate the AWS Agentless Discovery Connector VM in the vSphere client, right-click it, and select Open Console.
    2.  Log in as "ec2-user" with the password "ec2pass".
    3.  Run the sudo setup.rb command.
    4.  A menu will appear, choose “Reconfigure Network Settings”
     ![](/.attachments/DK-Portfolio/image2017-10-15_11-36-35.png)
    6.  In the “Reconfigure Network Settings” menu, choose “Set up a static IP”
     ![](/.attachments/DK-Portfolio/image2017-10-15_11-37-8.png)
    8.  Reboot the ADS connector (sudo reboot)

Create a Read-Only vCenter User and Control the Scope of Data Collection 
 

----------------------------------------------------------------------------

The vCenter user requires read-only permissions on each ESX host or virtual machine to inventory using the Application Discovery Service. Using the permission settings, you can control which hosts and VMs are included in data collection. You can either allow all hosts and VMs under the current vCenter to be inventoried, or grant permissions on a case-by-case basis. 
 

The following procedures describe configuration scenarios ordered from least granular to most granular. 

_Note: As a security best practice, we recommend against granting additional, unneeded permissions to the_ _vCenter_ _user._ 

### Discover data about all ESX hosts and virtual machines under the current vCenter 

1.  In your VMware vSphere client, choose vCenter and then choose either Hosts and Clusters or VMs and Templates.  
    
2.  Choose Manage, Permissions.
3.  Select the vCenter user, open the context (right-click) menu, and choose Change Role. 
    
4.  In the Assigned Role pane, choose Read-only.
5.  Select Propagate to children and choose OK.

### Discover data about a specific ESX host and all of its child objects 

1.  In your VMware vSphere client, choose vCenter and then choose either Hosts and Clusters or VMs and Templates.  
    
2.  Choose Related Objects, Hosts.
3.  Open the context (right-click) menu for the host name and choose All vCenterActions, Add Permission. 
    
4.  Under Add Permission, add the vCenter user to the host. For Assigned Role, choose Read-only.  
    
5.  Select Propagate to children and choose OK.

### Discover data about a specific ESX host or child VM 

1.  In your VMware vSphere client, choose vCenter and then choose either Hosts and Clusters or VMs and Templates.  
    
2.  Choose Related Objects.
3.  Choose Hosts (showing a list of ESX hosts known to vCenter) or Virtual Machines (showing a list of VMs across all ESX hosts). 
4.  Open the context (right-click) menu for the host or virtual machine name and choose All vCenterActions, Add Permission. 
    
5.  Under Add Permission, add the vCenteruser to the host or VM. For Assigned Role, choose Read-only.  
    
6.  Choose OK. 

_Note:_ If you selected the Propagate to children option, you can still remove the read-only permission from ESX hosts and VMs on a case-by-case basis. This option has no effect on inherited permissions applying to other ESX hosts and VMs.  

Create and Configure an IAM User 

----------------------------------

The Application Discovery Service uses the following IAM managed policies to control access to the service or components of the service. For information about how to attach managed policies to an IAM user account, see [Working with Managed Policies](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-using.html). 

*   **AWSAgentlessDiscoveryService**\- Grants the AWS Agentless Discovery Connector running in your VMware vCenter Server access to register, communicate with, and share connector health metrics with Application Discovery Service. This policy should be attached to any user whose credentials are to be used by the connector. 
    

The following additional Managed Policies **are not required** to implement the ADS Connector. 

*   **AWSApplicationDiscoveryServiceFullAccess**\- Grants the IAM user account access to the Application Discovery Service API. With this policy, the user can configure Application Discovery Service, start and stop agents, start and stop agentless discovery, and query data from the AWS Discovery Service database. This policy also grants the user access to Arsenal. Arsenal is an agent service managed and hosted by AWS that forwards data to Application Discovery Service in the cloud. 
    
*   **AWSApplicationDiscoveryAgentAccess**\- Grants the AWS Application Discovery Agent access to register and communicate with Application Discovery Service. This policy should be attached to any user whose credentials are to be used by an AWS Application Discovery Agent. 

### Create IAM User in the Customer’s Target AWS Account and Attach Required IAM User Policies

1.  Sign in to the Target AWS Account
2.  Go to **IAM** Console
 ![](/.attachments/DK-Portfolio/image2017-10-15_11-42-57.png)
4.  Click **Users** and then **Add user**
 ![](/.attachments/DK-Portfolio/image2017-10-15_11-42-26.png)
6.  Type in **AWS-ApplicationDiscoveryService** in **User name** field, Check the box next to **Programmatic access**, and Click **Next: Permissions**
 ![](/.attachments/DK-Portfolio/image2017-10-15_11-41-25.png)
8.  Click **Attach existing policies directly**, Filter on and check the box next to the **AWSAgentlessDiscoveryService,** and Click **Next: Review**
 ![](/.attachments/DK-Portfolio/image2017-10-15_11-40-47.png)
10.  Click **Create User**
11.  Click **Download .csv** and store the file in your organizations secrets repository (e.g. CybeArk, etc.)
13.  Click **Close**

### Configuring the AWS Agentless Discovery Connector 

To finish the setup process, open a web browser and configure the connector using the console.

1.  In a web browser, type the following URL in the address bar: [https://ip\_address/](https://ip_address/), where ip\_addressis the IP address of the connector console that you saved earlier.  
    
2.  Choose Get started now.
3.  In Step 1: License Agreement, read and accept the agreement and choose Next.
4.  In Step 2: Create a Password, type a strong password for access to the connector and choose Next.
5.  In Step 3: Network Info, read the information provided and configure network settings. 
6.  In Step 4: Log Uploads & Upgrades, select the desired options and choose Next.
7.  In Step 5: Discovery Connector Set Up, choose Configure vCenter
    1.  For vCenterHost, type the hostname or IP address of your VMware vCenter Server host. 
        
    2.  For vCenterUsername, type the name of a local or domain user that the connector uses to communicate with vCenter. For domain users, use the form domain\\username or username@domain. 
        
    3.  For vCenterPassword, type the user password. 
        
    4.  **Choose Ignore security certificate** to bypass SSL certificate validation with vCenter.
8.  Choose Configure AWS credentials and type the credentials for the IAM user who is assigned theAWSAgentlessDiscoveryServiceIAM policy that you created in [Attach Required IAM User Policies](http://docs.aws.amazon.com/application-discovery/latest/userguide/create-iam-user.html#appdisc-user-policy). Choose Next. 
    
9.  Choose Configure where to publish data and select suitable publishing options. Choose Next. You should see the AWS Agentless Discovery Connector console.

_After you complete this initial setup, you can access connector settings by using SSH and the connector IP address:_ _root@__Connector\_IP\_address. The default user name is ec2-user and the default password is ec2pass._ **_We strongly encourage you to change the value of the default user name and password._**

Collecting and Exporting Data 

===============================

After agentless-discovery setup is complete, you can use the console or API to start collecting data; managing service, tag, and query configuration items; and exporting data. You can export data as a CSV file to an Amazon S3 bucket or an application that enables you to view and evaluate the data. For more information, see [Tutorial: Using the AWS Application Discovery Service Console](http://docs.aws.amazon.com/application-discovery/latest/userguide/console_walkthrough.html) or the [Application Discovery Service API Reference](http://docs.aws.amazon.com/application-discovery/latest/APIReference/). 

### To start data collection for both agents and connectors

1.  Sign in to the Target AWS Account

1.  Go to the **Application Discovery Service** console
2.  In the navigation menu, choose **Data collection**, **Connector**.
3.  In the table, select the check box associated with each of the agents to start.
4.  Choose **Start data collection**. In the **Collection status** field, note that the status of each of your selected collection tools changes to either **START\_SCHEDULED** or **STARTED**. The next time each of your selected collection tools contacts AWS, it collects and sends data to Application Discovery Service.

### To stop data collection

1.  In the navigation menu, choose **Data collection**, **Connector**.
2.  In the table, select the check box associated with each of the agents to stop.
3.  Choose **Stop data collection**. In the **Collection status** field, note that the status of each of your selected collection tools is now either **STOP\_SCHEDULED** or **STOPPED**. The next time each of your selected collections tools contacts AWS, it stops sending discovery data to Application Discovery Service. The status of each selected collection tool changes to **STOPPED** after data collection has halted.

Export Data to CSV file
-----------------------

1.  Ensure awscli is at version 1.11.138 or higher
    1.  **awscli** **\--version**
2.  Run **aws discovery start-export-task --region us-west-2**
3.  Run **aws discovery describe-export-tasks --region us-west-2**
4.  Download the zip file using the **configurationsDownloadUrl** link entry in the **describe-export-tasks** output

Set up AWS Application Discovery Agents (Optional at a future point in time) 

==============================================================================

Discovery Agents will not be used during the initial implementation of the AWS Discovery Service. If needed, the instructions for implementing discovery agents can be found here: [http://docs.aws.amazon.com/application-discovery/latest/userguide/setting-up-agents.html](http://docs.aws.amazon.com/application-discovery/latest/userguide/setting-up-agents.html) 
 

ADS References 

================

ADS Overview: [https://aws.amazon.com/application-discovery/](https://aws.amazon.com/application-discovery/) 
 

ADS FAQ: [https://aws.amazon.com/application-discovery/faqs/](https://aws.amazon.com/application-discovery/faqs/) 
 

ADS User Guide: [http://docs.aws.amazon.com/application-discovery/latest/userguide/what-is-appdiscovery.html](http://docs.aws.amazon.com/application-discovery/latest/userguide/what-is-appdiscovery.html)

 **Attachments:** 


[image2017-10-15_11-36-35.png](/.attachments/DK-Portfolio/image2017-10-15_11-36-35.png)

[image2017-10-15_11-37-8.png](/.attachments/DK-Portfolio/image2017-10-15_11-37-8.png)

[image2017-10-15_11-40-15.png](/.attachments/DK-Portfolio/image2017-10-15_11-40-15.png)

[image2017-10-15_11-40-47.png](/.attachments/DK-Portfolio/image2017-10-15_11-40-47.png)

[image2017-10-15_11-41-25.png](/.attachments/DK-Portfolio/image2017-10-15_11-41-25.png)

[image2017-10-15_11-42-26.png](/.attachments/DK-Portfolio/image2017-10-15_11-42-26.png)

[image2017-10-15_11-42-57.png](/.attachments/DK-Portfolio/image2017-10-15_11-42-57.png)
