  

**Document Lifecycle Status**

|    |    |    |    |
| --- | --- | --- | --- |

  

  

  

[[_TOC_]]

* * *

Introduction
============

Welcome to the AWS Managed Services (AMS) Application Design Questionnaire. This questionnaire is used to describe the deployment elements and structure so that AMS can determine the infrastructure components needed in the target state design. One template should be completed per application/workload; AWS Professional Services will combine the data submitted in each template and produce a migration report from the data provided. 

Use this questionnaire to describe your deployment elements and structure so AMS can determine what infrastructure components are needed in the target state design. The onboarding requirements for Line-of-Business applications are significantly different than Product applications, so this questionnaire is designed to address both.

System Overview Diagrams & Other Application Artifacts
======================================================

Linked Artifacts
----------------

|   Name   |   Description   |   Link   |
| --- | --- | --- |
|         |         |         |
|         |         |         |

Directions
==========

Application Owners
------------------

An application owners (or workload owner) is the group or individual that is responsible for the program or programs, which make up the application/workload and is responsible for the development, test, and production of the application/workload that meets a set of requirements and objectives.

Application owners should answer questions identified by: (AO)

Workload
========

Deployment Summary
------------------

  

|   **1.0 Deployment Summary**   |
| --- |
|   **1.1 Is this application considered a Line-of-Business application or a Product application?** (AO)   |
|   _A Line-of-Business application is an applications used to create and manage your Product applications_  _A Product application serves the end customer_  * * *  -  Line-of-Business -  Product  _Please add any details as necessary:_        |
|   **1.2 Will this deployment require an auto-scaled ARP (authenticated reverse proxy) within the account’s public/DMZ subnet?** (AO)    |
|   _An authenticated reverse proxy is a reverse proxy that only retrieves the resources on behalf of a client if the client has been authenticated. If a client is not authenticated they can be redirected to a login page._  * * *  -  Yes -  No  _Please add any details as necessary:_        |
|   **1.3 Will servers be deployed within the account’s public/DMZ subnet, or will both Web and application servers be deployed within the account's private subnet?** (AO)    |
|   _AMS subnet: A managed subnet that resides in a VPC. In a typical AMS account, three subnets are mirrored across two availability zones:_  *   _DMZ subnets connect your internet gateway and private subnets. They contain a route to the internet gateway and also a managed NAT that allows resources in the private subnets to communicate with the internet. Public-facing resources can also be provisioned in the DMZ subnets, such as a managed public load balancer that receives HTTP/HTTPS requests to be forwarded to resources in the private subnets_      *   _Shared services subnets are accessible to and from the DMZ and your private subnet. Shared services include access management services for DNS and bastions to access managed resources; security management services including EPS, security groups, and user permissions; and change management services such as patching, continuity, monitoring, and logging._      *   _Private, or Customer Application subnets for your internal applications and databases, accessible from your corporate network, DMZ, and the AMS shared services subnets._       * * *  -  Servers will be deployed within the account’s public/DMZ subnet -  All servers will be deployed within the account’s private subnet  _Please add any details as necessary:_        |
|   **1.5 Are the servers (ARP, web, application, database, load balancer, etc.) separated into distinct security groups?** (AO)   |
|   _Security groups: Virtual firewalls for your instance to control inbound and outbound traffic. Security groups act at the instance level, not the subnet level. Therefore, each instance in a subnet in your VPC could be assigned to a different set of security groups. Your AMS-managed VPC has a default security group that allows web access._  * * *  -  Yes -  No  _Please add any details as necessary:_        |
|   **1.6 Will this environment require a HA (high availability) design spread across availability zones (AZs) i.e. "Multi-AZ".** (AO)   |
|   -  Yes -  No  _Please add any details as necessary:_        |

Infrastructure Deployment Components
------------------------------------

|   **2.0 Infrastructure Deployment Components**   |
| --- |
|   **2.1 Region: What AWS region or regions are needed?** (AO)   |
|   _AMS operates in a subset of all AWS Regions; however, the AMS API/CLI runs out of the "USA East (N. Virginia)" region only. For the most recent AMS supported AWS Regions, see the_ [_AWS Managed Services Service Description_](https://s3.amazonaws.com/ams.contract.docs/AWS+Managed+Services+Service+Description.pdf)_, which can be found at the bottom of the left column of the main Documentation index page. AMS multi-account is constrained to AWS Regions that support Transit Gateway, if Direct Connect is used._  * * *      _Please add any details as necessary:_        |
|   **2.2 High Availability (HA): How many availability zones will be used?** (AO)   |
|   _Each Region has multiple, isolated locations known as Availability Zones. When you launch an instance, you can select an Availability Zone or let us choose one for you. If you distribute your instances across multiple Availability Zones and one instance fails, you can design your application so that an instance in another Availability Zone can handle requests. See_ [_here_](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html#concepts-availability-zones) _for more details._  * * *      _Please add any details as necessary:_        |
|   **2.3 Virtual Private Cloud (VPC): What is the CIDR block for the VPC for this particular environment?** (AO)   |
|   _Amazon Virtual Private Cloud (Amazon VPC) enables you to define a virtual network in your own logically isolated area within the AWS cloud, known as a virtual private cloud (VPC). You can launch your Amazon EC2 resources, such as instances, into the subnets of your VPC. Your VPC closely resembles a traditional network that you might operate in your own data center, with the benefits of using scalable infrastructure from AWS. You can configure your VPC; you can select its IP address range, create subnets, and configure route tables, network gateways, and security settings. You can connect instances in your VPC to the internet or to your own data center. See_ [_here_](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-vpc.html) _for more details._  * * *         _Please add any details as necessary:_            |
|   **2.4 If an Authenticated Reverse Proxy (ARP) is required, please provide the associated details below: (AO)**   |
|   *   OS:       *   AMI:       -  Amazon Linux 2 (Latest Minor Release) -  Amazon Linux (Latest 2018.03 Release) -  Red Hat Enterprise 6 (Latest Minor Release) -  Red Hat Enterprise 7 (Latest Minor Release) -  SUSE Linux Enterprise Server 12 SP4 -  SUSE Linux Enterprise Server 15 SP1 -  CentOS 6 (Latest Minor Release) -  CentOS 7 (Latest Minor Release) -  Microsoft Windows Server 2008 R2 -  Microsoft Windows Server 2012 -  Microsoft Windows Server 2012 R2 -  Microsoft Windows Server 2016 -  Microsoft Windows Server 2019  *   Instance type (see [here](https://aws.amazon.com/ec2/instance-types/) for a list of current available instance types):      *   Subnet ID:      *   Security Group:      *   Ingress port:        |
|   **2.5 If an Application Deployment Tool server is required, please provide the associated details below: (AO)**   |
|      _Please add any details as necessary:_        |
|   **2.6 If AWS RDS with MySQL is required, please provide the associated details below: **(AO)****   |
|   *   DB version:      *   Usage Type:      *   Instance class:      *   Subnet ID:      *   Security group:      *   DB instance ID:      *   Storage size:      *   Multi-AZ:      *   Auth type:      *   Encryption:        |
|   **2.7 Is your application stateless? ****(AO)******   |
|   -  Yes -  No  _Please add any details as necessary:_        |
|   **2.8 Do you require S3 buckets? ******(AO)********   |
|   -  Yes -  No  _Please add any details as necessary:_        |
|   **2.9 Do you require persistent storage? ********(AO)**********   |
|   -  Yes -  No  _Please add any details as necessary:_        |
|   **2.10 Do you require data at rest encryption on your EBS volumes? ********(AO)**********   |
|   -  Yes -  No  _Please add any details as necessary:_        |
|   **2.11 Do you require DB encryption? ********(AO)**********   |
|   -  Yes -  No  _Please add any details as necessary:_        |
|   **2.12 Does your application require External (to the Managed Services VPC) server endpoints? ********(AO)**********   |
|   -  SMTP -  LDAP -  SFTP -  Others (please specify):   |
|   **2.13 Will your application require Network filtering? ********(AO)**********   |
|   -  Yes -  No  _Please add any details as necessary:_        |
|   **2.14 Will your application require Web traffic inspection (inbound?outbound?)? ********(AO)**********   |
|   -  Yes -  No  _Please add any details as necessary:_        |
|   **2.15: Tagging: What tags should be used to group resources into logical collections? ********(AO)**********   |
|   _For example, all resources for an application stack. Select tags for your use case; for example, backup=true to enable backups. Additionally, you must use the tag “name=value” in order for any EC2 instances you create to display a name in the console._  Example:  *   Tag 1: Attach to all Production EC2 instances          *   Key: Environment              *   Value: PROD           * * *  *   Tag 1:          *   Key:              *   Value:           *   Tag 2:          *   Key:              *   Value:            |
|   **2.16 What security groups are needed for your application? ********(AO)**********   |
|   _Security Groups are Virtual firewalls for your instance to control inbound and outbound traffic. Security groups act at the instance level, not the subnet level. Therefore, each instance in a subnet in your VPC could be assigned to a different set of security groups. Your AMS-managed VPC has a default security group that allows web access._  Example:  Security Group 1: Attach to all Web tier EC2 instances  *   Ingress Rules:          *   22 from 10.12.12.1              *   443 from 10.1.1.1          *   Egress Rules:          *   All ports to 0.0.0.0/0           * * *  *   Security Group 1:          *   Ingress rules:              *   Egress rules:          *   Security Group 2:          *   Ingress rules:              *   Egress rules:                 |

Application Hosting Platform
----------------------------

|   **3.0 Application Hosting Platform**   |
| --- |
|   **3.1 Will Databases be encrypted?** (AO)   |
|   -  Yes -  No  _Please add any details as necessary:_        |
|   **3.2 Who will manage Encryption keys? (AO)**   |
|   Name:  Email:  Team:   |
|   **3.3 Will all data in-transit and at-rest be encrypted?** (AO)   |
|   -  Yes -  No  _Please add any details as necessary:_        |
|   **3.4 Will all user access to the system be via HTTPS?** (AO)   |
|   -  Yes -  No  _Please add any details as necessary:_        |
|   **3.5 Will all system-to-system interactions be approved by your security Operations team? (AO)**   |
|   -  Yes -  No  _Please add any details as necessary:_        |

Application Deployment Model
----------------------------

|   **4.0 Application Deployment Model**   |
| --- |
|   **4.1 Are your deployments automated or manual? (AO)**   |
|   _No deployment automation implies no Auto Scaling in AMS. If you request access and log in and manually update your application, and your update fails, AMS would expect you to rollback your update or alert us through a service request so we can assist you._  * * *  -  Automated -  Manual  _Please add any details as necessary:_        |
|   **4.2 If your deployments are automated, what is the framework?**  (AO)   |
|   _Agent-based and agentless deployment tooling require a separate instance be created and deployed as the master server for the tooling. AMS expects you to be aware of all of the elements necessary for successful application deployment tooling; however, we are happy to help with related infrastructure questions._  * * *  -  Scripts -  Agent-based (puppet/chef) -  Agentless (SALT/Ansible) -  CodeDeploy -  Other (please specify):  _Please add any details as necessary:_        |
|   **4.3 Do your Line-of-Business applications (those applications that you use to create and manage your applications) require patching? (AO)**   |
|   -  Yes -  No  _Please add any details as necessary:_   |

Application Dependencies
------------------------

|   **5.0 Application Dependencies**   |
| --- |
|   **5.1 What Network-level dependencies do your Applications require to function properly?**   |
|   _For example, AWS DirectConnect_  * * *            |
|   **5.2 What package dependencies does your Application require to function properly?**(AO)   |
|   _For example, pip_  * * *            |
|   **5.3 What other applications are required for your Application to function properly?** (AO)   |
|   _For example, MySql_  * * *            |
|   **5.4 Do any firewall dependencies exist for your Application to function properly?** (AO)    |
| -  Yes -  No  * * *  _Please provide details_  * * *            |

**SSL Certificates for Product Applications**
---------------------------------------------

|   **6.0 SSL Certificates for Product Applications**   |
| --- |
|   6.1 **What SSL certificates will your servers need so your applications (LoB and product) can reach everything they need to run and be accessible?** (AO)   |
|   _As an example, for each of the instances listed above you might need the following certificates:_  _WAF (cert 1) - > ELB-Ext (cert 2) - > ARP (cert 3) - > ELB-Int (cert 4) -> Website (cert 5) - > ELB-Int (cert 6) -> Web service (cert 7)._  * * *  *   **Auto Scaling Group?**      *   **Database (RDS)?**      *   **Load Balancer?**      *   **Deployment tool server?**      *   **Web application firewall (WAF)?**      *   **Other instances?**        |

 **Attachments:** 


[Application%20DB%20Mapping%20Template%20-%20Blank%20Databases.xlsx](/.attachments/DK-Portfolio/Application%20DB%20Mapping%20Template%20-%20Blank%20Databases.xlsx)
