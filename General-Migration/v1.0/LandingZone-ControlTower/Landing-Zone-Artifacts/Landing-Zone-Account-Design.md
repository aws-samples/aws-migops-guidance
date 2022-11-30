  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

Purpose
=======

This page captures the design details for the customer's landing zone accounts. This is a reference implementation for the Landing Zone that should be customized during design workshops to meet the specific needs of the customer.

AWS Organizations Matrix
========================

|   **Account Name**   |   **OU Name**   |   **Role**   |   **Email**   | Support Levels |  Billing Contact | Operations Contact | Security Contact |   **Account ID**   | Account Alias |   **Organization ID**   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|   Billing   |   Core   |   Master Billing OU & Account   |   aws-master@acme.org   | Business |   Full Name:   Title:  Email: [aws-billing@acme.org](mailto:aws-billing@acme.org)  Phone #:   |   Full Name:   Title:  Email: [aws-operations@acme.org](mailto:aws-operations@acme.org)  Phone #:   |   Full Name:   Title:  Email: [aws-soc@acme.org](mailto:aws-soc@acme.org)  Phone #:   |   xxxxxxxxxxxx   |     |   x-xxxxxxxxxx   |
|   Log archive   |   Core   |   Central security log aggregation account   |   aws-log-archive@acme.org   | Business |     |     |     |   xxxxxxxxxxxx   |     |   NA   |
| Audit |   Core   | Central Security Discovery and Management Account | aws-audit@acme.org | Business |     |     |     | xxxxxxxxxxxx |     | NA |
| Security | Core | Central Security account for Guard Duty, SNS and Config Aggregator | aws-security@acme.org | Business |     |     |     | xxxxxxxxxxxx |     | NA |
|   Shared Services   |   Shared   |   Central Shared Services/platform workloads   |   aws-ss@acme.org   | Business |     |     |     |   xxxxxxxxxxxx   |     |   NA   |
|   Dev   |   Dev   |   Development workloads   |   aws-dev@acme.org   | Business |     |     |     |   xxxxxxxxxxxx   |     |   NA   |
|   Test   |   Test   |   Test workloads   |   aws-test@acme.org   | Business |     |     |     |   xxxxxxxxxxxx   |     |   NA   |
|   Prod   |   Prod   |   Production workloads   |   aws-prod@acme.org   | Business |     |     |     |   xxxxxxxxxxxx   |     |   NA   |
|   Sandbox   |   Sandbox   |   Used for Infrastructure Development/Automation testing   | aws-sandbox@acme.org    | Business |     |     |     |   xxxxxxxxxxxx   |     |   NA   |
| Transit | Shared | Central networking resources. DX, Ingress, Egress, Client VPN, etc. | aws-transit@[acme.org](http://acme.org) | Business |     |     |     | xxxxxxxxxxxx |     | NA |

AWS SSO and IAM Login Links
---------------------------

| Account Name | Link |
| --- | --- |
| Acme Landing Zone AWS SSO Login |   [https://acme.awsapps.com/start](https://acme.awsapps.com/start)   |
| Master Billing IAM Login |   [https://111111111111.signin.aws.amazon.com/console/](https://111111111111.signin.aws.amazon.com/console/)   |

  

Naming Conventions
------------------

|   **Object**   |   **Naming Convention**   |   **Example**   |
| --- | --- | --- |
|   Organization Name   |   Use the standard Org Name   |   Acme   |
|   Organization Unit Name   |   Match the Landing Zone reference names   |   *   Acme        *   Core     *   Shared     *   Dev     *   Test     *   Prod     *   Sandbox   |
|   AWS Account Name   |   Match the Landing Zone reference names   |   *   Acme *   Log archive *   Audit *   SharedServices *   Dev *   Test *   Prod *   Sandbox   |
|   AWS Account Email Alias   |   aws-{AccountName}@{OrgEmailDomain}   |   aws-prod@acme,org   |

AWS Accounts & VPCs Diagram
===========================

  

Master Billing Account
======================

This account is the account that pays all other accounts. It can be either a single account for the entire organization or a separate account for every Line of Business (LOB) within the organization. The rest of the accounts will be linked to this billing account via consolidated billing. The billing account will store detailed billing reports for all accounts, analyze the AWS usage and spend and set billing alarms (or a budget) to provide notification in case of any threshold breach.  
Additionally, the billing account serves as the AWS Organizations master account, and this master account provides the capability to create other AWS accounts. Every new account created is automatically linked to the master account for consolidated billing. The master account should host the Cross-Account Manager solution which automates account management including account creation and bootstrapping.  
This account should not deploy any application workloads, it should only deploy solutions or tools for account and cost management only.

|   **Owner**   |   CIO or LOB head   |
| --- | --- |
|   **Components**   |   *   AWS Organizations Master account *   S3 bucket to store DBR logs from all accounts *   Solutions: Control Tower for account management (creating and bootstrapping new accounts), and Cost Optimization Monitor (billing and cost analysis)   |

Log archive Account
===================

This account is for security and compliance-related logging and auditing activities. This account hosts the aggregated security logs from all accounts in a security logs bucket. The logs are then analyzed by Centralized Logging solution or a third-party log analysis tool. This account is also responsible for maintenance of the overall security posture of all accounts as it scans for vulnerabilities (i.e., ports open to the world) at periodic intervals. It may either take a corrective action or alert the user of any security or compliance events.

|   **Owner**   |   CISO (Security/Compliance Team)   |
| --- | --- |
|   **Components**   |   *   S3 bucket to store security logs from all other accounts; Versioning and MFA delete enabled *   Solutions: Control Tower   |

Audit Account
=============

This account is for security auditing activities. This account is also responsible for maintenance of the overall security posture of all accounts as it scans for vulnerabilities (i.e., ports open to the world) at periodic intervals. It may either take a corrective action or alert the user of any security or compliance events.

  

|   **Owner**   |   CISO (Security/Compliance Team)   |
| --- | --- |
|   **Components**   |   *   Read only cross-account role to all other accounts *   Write only cross-account role to all other accounts *   Solutions: Control Tower   |

Transit Network Account
=======================

This account act as the global network transit center connecting different VPCs (including ones that are potentially geographically dispersed) and remote networks.

  

|   **Owner**   |   Infrastructure/Network Team   |
| --- | --- |
|   **Components**   |   *   VPC to host Transit Gateway *   Direct Connect Termination *   VPN Site to Site Termination *   Centralized VPC Endpoints   |

  

Shared-services Account

This account hosts common services that can be shared by applications or workloads deployed in application accounts. It can be used to host golden AMIs or service catalog portfolios that are shared with application accounts. Additionally, this account can act as the global network transit center connecting different VPCs (including ones that are potentially geographically dispersed) and remote networks.

|   **Owner**   |   Infrastructure/Network Team   |
| --- | --- |
|   **Components**   |   *   VPC to host AD, DNS, etc., services; peered with application accounts; *   Service Catalog shared portfolio *   Golden AMI Repo *   Solutions: CI/CD pipeline, Backup Media Servers, etc.   |

Accounts by LOB, Applications, Projects
=======================================

Sandbox account
---------------

This is a time and financially-boxed experimental account for developers to try new services. It does not have connectivity to on-premises or VPC peering with the shared-services account.

Dev/Test Accounts
-----------------

These application accounts are used for development and testing. They offer network connectivity to on-premises, security baseline and VPC peering with the shared-services account.

Production Accounts
-------------------

These accounts host the production version of applications. They have a similar setup as the Dev/Test accounts with the highest level of security controls.

|   **Owner**   |   LOB/Application team   |
| --- | --- |
|   **Components**   |   *   VPC appropriate for workload (e.g. internal-only, internal and external, etc.) *   Customer workloads *   Solutions to manage cost and resilience: EC2 scheduler, EBS Snapshot, Limit Monitor, Cost Optimization Right Sizing.   |

* * *

### **AWS Support Levels**

It will be recommended when setting up accounts to select the correct AWS support level for the accounts.

By default all accounts are setup with basic support.  

Provided is a link to AWS Support levels including their feature and cost comparisons. 

[https://aws.amazon.com/premiumsupport/pricing/](https://aws.amazon.com/premiumsupport/pricing/)

 **Attachments:** 


[LandingZoneAccountVPC](/.attachments/DK-LandingZone-ControlTower/LandingZoneAccountVPC)

[LandingZoneAccountVPC.png](/.attachments/DK-LandingZone-ControlTower/LandingZoneAccountVPC.png)

[~LandingZoneAccountVPC.tmp](/.attachments/DK-LandingZone-ControlTower/~LandingZoneAccountVPC.tmp)
