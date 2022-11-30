  

**Document Lifecycle Status**

|    |    |    |    |
| --- | --- | --- | --- |

  

  

1.  Consider using the [MPA tool](http://mpa-proserve.amazonaws.com/) (available to AWS Employees and Partners) customizable ingestion questionnaires to automate the data ingestion process.
2.  Utilize this templates to conduct detailed application discovery assessments. 
3.  Review and revise the templates below with the customer to capture any specific information that is unique to their environment and to remove unnecessary information.
4.  For each application targeted for migration, make a copy of the revised template and have the customer fill it out.
5.  An alternative workbook is available as an attached file that can be downloaded. See Introduction section, alternative template.
6.  Load specific asset information (e.g., servers, databases, storage) into a common application and infrastructure inventory (e.g., **Template - Application and Infrastructure Inventory**)

[[_TOC_]]

* * *

Introduction
============

Welcome to the AWS Professional Services Application Discovery Template. This template can be used for entering key information about your application/workload to assist us in planning its migration to AWS. One template should be completed per application/workload; AWS Professional Services will combine the data submitted in each template and produce a migration report from the data provided. 

**Note:** 
depending on the migration strategy chosen for the applications, there could be significant variation in the level of detail required. For example, most Rehost strategies will require a simple design and less discovery details, the focus will be mainly in validating technology stack compatibility, operations, and security. On the other hand, a Refactor approach will require detailed designs and understanding of the application. Consider adapting the questionnaire to meet the level of complexity required by removing sections as needed. 

Alternative Template
--------------------

The attached workbook contains the same questions as the questionnaire below. This is available to be used as an alternative to the Confluence page. Specially to gain ability to accelerate ingestion of data into the inventory.

 [Application%20Detailed%20Discovery%20Questionnaire.xlsx](/.attachments/DK-Portfolio/Application%20Detailed%20Discovery%20Questionnaire.xlsx)

System Overview Diagrams & Other Application Artifacts
======================================================

Linked Artifacts
----------------

|   Name   |   Description   |   Link   |
| --- | --- | --- |
|         |         |         |
|         |         |         |

Contacts
========

Note: an application owner (or workload owner, or product owner) is the team or individual that is responsible for the strategic view, development, test, and production of the application/workload.

| Primary contact name | Role | email address | phone number |
| --- | --- | --- | --- |
|     | Application Owner |     |     |
|     | Application Developer |     |     |
|     | Application Operations |     |     |
|     | Infrastructure Operations |     |     |

Application/Workload
====================

1 - Application Overview
------------------------

|   1.1 Please provide an overview of the application/workload, business objective, its use case, its key purpose and any other information that is relevant to AWS understanding your application.   |
| --- |
|             |
| **1.1.1 Have previous application discoveries been performed, and if so, is the result available to be shared?** |
|             |
| **1.1.2 Does deep technical expertise in the application/workload exist with the current personnel resources, or are there gaps in knowledge? (ie - application was developed by a team no longer in the organization, insufficient documentation exists of the application, etc.)** |
|             |
|   1.2 What is the mission value level of the workload? (How important is this application)   |
| -  High (Mission Critical) -  Medium (Somehow important)  -  Low (Non-Mission Critical) -  Unknown |
|   1.3 What is the impact/blast radius of a failure in the application/workload? (e.g. who is affected if this goes down)   |
|             |
|   1.4 Who are the key users of the application/workload and how often do they utilize the application?   |
|             |
|   1.4.1 Please break down the users by region   |
|             |
|   1.5 What is your internal name/abbreviations for this application/workload? (What is this application commonly called)   |
|   _(Please also provide a unique ID if known/available)_  * * *            |
|   1.6 Is there any planned downtime or any outages anticipated for this application workload?   |
|             |
|   1.7 Is the workload approaching a technology refresh?   |
|   -  Yes -  No  If yes, Anticipated technology refresh date:    * * *  _Please provide details of the planned technology refresh_  * * *              |
|   1.8 How risky is this system? (Consider PII, data classification, public facing, internal only)   |
|   _Please describe the rationale for the selected level_  * * *  -  High (e.g., sensitive data, regulated, +99% SLA, internet facing) -  Medium (e.g., internet facing, 95-98% SLA, well-documented compliance requirements) -  Low (e.g., internal, non-sensitive data) -  Unknown        |
|   1.9 What is the complexity level of the workload? (e.g. how many other systems does this interface with)    |
|   _Please describe the rationale for the selected level_  * * *  -  Complex (e.g., +50 dependencies, legacy systems such as Mainframe, Unix, tight recovery times) -  Medium (e.g., 10-49 dependencies, few of them to legacy systems) -  Low (e.g., 0-9 dependencies, APIs, all systems supported in cloud) -  Unknown        |
|   1.10 Describe the number/type of environment(s) that exist to support this workload?   |
|   _e.g. Dev, Test, Staging, Prod, Disaster Recovery, etc._  * * *            |
|   1.11 Please define all internal/external URLs affected by migration. Document the DNS Forward and Reverse**, and provide a mapping of URL to end customer, if applicable.**   |
|   _e.g. Forward DNS:_ [_http://mydomain.doe.gov_](http://mydomain.doe.gov)      * * *  _Windows: nslookup -type=ptr w.x.y.z (enter your IP address in w.x.y.z) / Linux: host w.x.y.z (enter your IP address in w.x.y.z)_  * * *        |

2 - Application Geography & Performance
---------------------------------------

|   2.1 Please provide the location(s) (City, State) of the data center(s) in which the application/workload is deployed?   |
| --- |
|             |
|   2.2 Does your application/workload utilize a content delivery network to improve performance?   |
|   _(If so, please provide details) e.g. Akamai, Cloudfront_  * * *        |
|   2.3 Describe the application usage cycles (e.g. Mostly business hours, Monday through Friday)   |
|             |
| 2.4 What is the current application load like? (e.g., constant, spiky)  |
|                 |
| 2.5 How well can the application load be predicted? (e.g., can be predicted one year out, unpredictable) |
|             |

3 - Application/Workload Environment
------------------------------------

|   3.1 How does the user/client connect to the application/workload?    |
| --- |
|   _For example, is this a web application or is there a dedicated client application?_  * * *            |
|   3.2 How many concurrent users/clients use the application/workload?   |
|   Number of users: xx users        |
|   3.3 Does the application use specific software for reporting purposes?   |
|   _Please list any specific reporting software or functionality used. For example, Crystal Reports, Microsoft SQL Server Reporting Services, Business Objects, or other business intelligence tools?_            |
|   3.4 What protocol is used to access the workload (e.g. HTTP, HTTPS, SSH, RDP etc)?   |
|             |
| **3.5 Does the app have any batch jobs or any other jobs scheduled in the application or database servers?** |
|   -  Yes -  No  _Please add any details as necessary:_   |

4 - Application/Workload Architecture
-------------------------------------

|   4.1 Is the application n-tier by design?   |
| --- |
|   e.g. 2 tier = database & website, 3 tier, db, front end, application server  -  Yes -  No |
|   4.2 Please describe each application layer and its components.   |
|   Please provide architectural diagrams, if available.        |
|   4.3 Does the application/workload have a tightly-coupled architecture or loosely-coupled service oriented architecture (SOA)?   |
|   _We are interested in understanding how your application/workload is architected as this allows us to make recommendations around the best use of compute, storage and network resource based on the particular application/workload design pattern in use._   * * *            |
|   4.4 Is this application load balanced? If so, provide details.   |
|   _Is the load balanced application active/active or active/passive? Algorithm, SSL Offloading, Stickiness, etc._  * * *            |
|   4.5 Does this application use any caching (object, database, common calls)?   |
|   Does it require any components such as Reddis, Memcache, Oracle In-Memory Database, Casandra, Times Ten, and Coherence  * * *            |

  

5 - Development and Deployment Approach
---------------------------------------

|   5.1 what is the rate of change for this application? (e.g., is the application actively developed or is it maintained purely to meet operational requirements?   |
| --- |
| -  Actively Developed (e.g., changed every 6 months or less) -  Sporadic changes (e.g., once a year) -  Maintained Only (e.g., no application changes, infrastructure patches only) |
|   5.2 Describe your approach to software development in relation to the application/workload.   |
|   _We would like to understand your current approach to software development and how the application/workload is developed (if applicable). e.g. Agile, Waterfall_  * * *            |
|   5.3 Does the application have an end-of-life plan?   |
| -  Yes -  No  * * *  _Please provide details_   * * *            |
|   5.4 Does the workload have fixed change/release cycle? (e.g. patched every Thursday or once a month)   |
| -  Yes -  No  * * *  _Please provide details_  * * *            |
|   5.5 Please describe the application development cycles:   |
|    _For example, scheduled change freeze, maintenance window, blue/green_  * * *            |
|   5.6 What is your App Teams availability to assist in migrating the application?   |
|     _Please explain_  * * *            |
|   5.7 How is (Current Application Name) \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ deployed (Automated / Manually )?   |
|     _Please provide details and include information about internal code repositories_  * * *            |
|   5.8 How are your **database** **deployments** done (Automated / Manually)?   |
|    Are any specific tool chains used for database updates (ie – redgate, liquibase, flywheel, etc)? _Please provide details._  * * *            |
|   5.9 What is the current tool chain used for first deployments/fresh **Application** **Deployment** (Continuous Integration / Continuous Delivery / Continuous Deployment)?   |
|    Examples: TeamCity, Aritfactory, Gitlab, Github, Octopus, Final Builder  What branch strategy is used? Do you have a list; can we obtain a list of the branch strategy for application deployment_?_  * * *            |
|   5.10 What is the current tool chain used for **Application** **Updates (**Code Updates, Code Changes, Releases/Patches**)** (Continuous Integration / Continuous Delivery / Continuous Deployment)?   |
|    Examples: TeamCity, Aritfactory, Gitlab, Github, Octopus, Final Builder  What branch strategy is used? Do you have a list; can we obtain a list of the branch strategy for application deployment?  * * *            |
|   5.11 What is the current tool chain used for **Infrastructure** **Deployment** (Continuous Integration / Continuous Delivery / Continuous Deployment)?   |
|    Examples: Chef, Puppet, Ansible, SALT   What branch strategy is used? Do you have a list; can we obtain a list of the branch strategy for infrastructure deployment  * * *            |
|   5.12 Do your CI/CD tools have licensing constraints?   |
|     _Please explain_  * * *            |
|   5.13 Is historical build information important to your application? (Yes/No)?   |
|     _Please explain_  * * *            |
|   5.14 Where are your CI/CD Tools installed/running? Who owns CI/CD for this application?   |
|    Are your CI/CD tools installed on a physical/virtual server you own or host? Is your CI/CD server in the CMDB? What is the current DNS name of your repositories that will be migrated to AWS? _Please provide details_  * * *            |
|   5.15 During your infrastructure / application deployments, are specific user accounts required?   |
|     Specify if special AD creds/dependencies are needed  * * *            |
|   5.16 For your application deployments, what steps are not or cannot be automated?   |
|     _Please explain_  * * *            |
|   **5.17 Is your application containerized?**   |
|   _If yes, what is the current and desired ochestration method?_  * * *            |

6 - Licensing
-------------

|   6.1 Please describe the software licensing requirements of the application/workload.   |
| --- |
|   _Please provide detail about software licenses required to run the application/workload in AWS as well as detail about any OS/database licensing requirements. Is the license portable? Licensed by core?_  * * *            |
|   6.2 Are there any other licensing considerations?   |
|   _For example, is there a requirement to upgrade versions of OSs as part of the migration?_  * * *            |
|   6.3 Please list any commercial off-the-shelf software used by the workload:    |
|   _Please list one application per line using the following structure: vendor, app, version, license expiry, update/update/retire due, due date (e.g. IBM, file net p8 content manager, 5.2,_ _, upgrade,_    * * *              |

7 - Migration
-------------

|   7.1 Please describe the preferred method of migration to AWS, if any.   |
| --- |
|   _We would like to establish here how you would like your migration to take place. For example, is there a preferred method of migration such as refactor, replatform, rehost._  * * *            |
|   7.2 Is downtime permitted for the application/migration to take place? (e.g., any preferred dates/time)   |
|   _Please provide details as to regular downtime windows, if any extensions to regular windows are possible, and any contractual constraints._  * * *            |
|   7.3 Please describe any considerations for the migration.   |
|             |
| **7.4 Please list the owner(s) of customer communication/coordination in relation to application changes, upgrades, and migrations (UAT, Cutover planning, etc)** |
|             |
| **7.5 Please describe the Customer Communication/Coordination requirements and procedures during application changes, upgrades, and migrations. Please describe any anticipated/common challenges.** |
|             |

8 - Testing
-----------

|   8.1 What are the current test mechanisms?   |
| --- |
|   Please provide details  * * *            |
|   8.2 Please describe the current test stages. (e.g., QA, UAT)   |
|   Please provide details  * * *            |

9 - Resources
-------------

|   9.1 Please provide a high-level summary of the key personnel you are able to make available to support the application migration.   |
| --- |
|   _Please include details of roles and responsibilities as well as any third party resources (non-AWS) that you anticipate requiring for the migration._  * * *            |
|   9.2 What costs for these resources do you anticipate?   |
|   _Please provide as much detail as possible about anticipated resource costs. e.g. extra contractor hours_  * * *            |

  
10 - Service Level Agreement (SLA)
-------------------------------------

|   10.1 Does the application/workload currently operate to defined SLA's?   |
| --- |
| -  Yes -  No  * * *  _Please describe key performance requirements for the application (if any, total number of users, concurrent users, transactions per seconds, throughput, response time, processing time, minimum availability), and if these requirements are contractual or not._  * * *            |
|   10.2 Does the application/workload have support provided internally or through a third party?   |
| -  Yes -  No  * * *  _Please provide details of the support being provided for the application/workload_  * * *            |
|   10.3 Have there been any workload/application/Infrastructure outages in the past 12 months?   |
| -  Yes -  No  * * *  _Please provide details e.g. system capacity issues, configuration issues, connectivity issues and identify the root cause_  * * *            |

11 - Compliance & Data Sovereignty
----------------------------------

|   11.1 Are there any compliance frameworks that the application/workload operates under?   |
| --- |
| -  SOC1 -  SOC2 -  SOC3 -  ISO 27001 -  ISO 27017 -  ISO 27018 -  ISO 9001 -  PCI -  FedRAMP -  HIPAA  * * *  _Provide narrative here about the compliance frameworks that apply, for example, if PCI application, can you provide a network flow diagram of all credit card data?_  * * *            |
|   11.2 Please provide the dates of the last audits for each compliance framework (if applicable)   |
|   SOC1:  SOC2:   SOC3:   ISO 27001:  ISO 27017:  ISO 27018:  ISO 9001:  PCI:  FedRAMP:  HIPAA:       |

12 - Dependencies
-----------------

|   12.1 Are there any dependencies on other centralized or shared services/applications (e.g. DNS, AD Authentication, etc)?   |
| --- |
|   This is mean to gather what this application needs to operate.        |
|   12.2 Are there any application dependencies that this application has in order to be migrated?   |
|    _This is to gather what OTHER applications require this application to operate. _Please describe each dependency (real-time, batch) and provide any data (operations per second, bytes per second/operation, etc) if available.__  __Please specify whether the dependency is Soft (i.e., can continue over WAN links such as Direct Connect) or Hard (i.e., the dependency cannot be resolved and must migrate alongside the dependant application)__  * * *            |
| **12.2.1 Are any of the above dependencies latency-sensitive? please specify the latency requirement** |
|                 |
|   **12.3 List of System Interfaces**   |
|   _Please provide a list of systems with which this system interfaces and the interface protocol (i.e. Oracle database link, LDAP, SOAP, RESTFul, SCIM)_  * * *        |
|   **12.4 System Interconnection Agreements**   |
|   _For each system listed in 11.3, do you have a security agreement with the interfaced system owner that would need modification?_  * * *            |
| **12.5 Are there any dependencies with Active Directory?** |
|   -   Yes -  App will not work after domain change -  App uses domain user/computer as a service account and uses customized SPN -  App saves app info in AD object -  App uses AD configuration partition or schema extension -  App is dependent on cross-domain authentication & authorization -  App is dependent on the group policy -  App is dependent on startup/login script -  App uses certificates issued by Windows CA server -  No  Please Explain            |

13 - Data
---------

|   13.1 Does the application data contain PII data?   |
| --- |
| -  Yes -  No |
|   13.2 Does the application data contain sensitive data? (controlled unclassified / Official Use Only)   |
| -  Yes -  No |
|   13.3 What is the data classification of the data?   |
| -  Public -  For Official Use Only (FOUO) -  Personal Identifiable Information (PII) -  Unclassified Controlled Nuclear Information (UCNI) -  ITAR (International Traffic in Arms Regulations) |
|   13.4 How do you currently transfer files to the server?   |
| -  RDP -  FTP / SFTP -  SSH / SCP -  Network Shares -  Repositories -  Other: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |
|   **13.5 From where do you currently transfer files to the server?**   |
| -  Non-Government Furnished Equipment (GFE) -  EITS Desktop -  Non-EITS Desktop -  Internet |

14 - Monitoring & Operations
----------------------------

|   14.1 Does the workload have a monitoring solution in place?   |
| --- |
| -  Yes -  No   * * *  _Please provide details of the monitoring solution used _and where logs are stored__  * * *            |
|   14.2 Does the workload have a backup process in place?   |
| -  Yes -  No   * * *  _Please provide details of the backup process used_  * * *            |
|   14.3 Are there change control procedures in place for this workload?   |
| -  Yes -  No   * * *  _Please provide details of the change control process used_  * * *            |

15 - Resiliency
---------------

|   15.1 Does your application have high availability and fault tolerance configurations?   |
| --- |
|   Please provide details  * * *            |
|   15.2 Does your application have Disaster Recovery configurations?   |
|   _Please provide details._  * * *            |
|   **15.2 What is the Recovery Point Objective (RPO) of the application?**   |
|   _Determines how often data should be backed up and how much data can be lost between backups if a crash occurs_  * * *  RPO: xx minutes        |
|   **15.3 What is the Recovery Time Objective (RTO) of the application?**   |
|   _Determines the target time for the recovery of the application/workload after a system disaster has struck. How long til the system has to be up._  * * *  RTO: xx minutes        |

16 - Application Security
-------------------------

|   16.1 Is your application currently encrypted in transit and at rest between all tiers?   |
| --- |
|   Is end-to-end encryption a requirement.        |
|   16.2 Does your application use any insecure protocols between tiers? (FTP, HTTP)   |
|   _Please provide details._  * * *            |
|   **16.3 Does your application traverse traffic globally or just within a certain region?**   |
|   _Are restrictions required, is a CDN required, etc._  * * *        |
|   **16.4 Can you describe Client Authentication requirements? ( Server Certificates, Client Certificates, User Authentication, SAML)**   |
|   _How does the application perform AAA?   _If SAML, please list identity provider details.__  * * *            |

Assets
======

Consider loading the information directly into **Template - Application and Infrastructure Inventory**

Compute
-------

In this section please provide as much information as possible about the compute resources assigned to this application/workload.

### Physical Servers

Enter details below for each of the physical servers that make up the application/workload. Do not include physical hosts that run a virtual machine hypervisor.

|   Hostname   | OS Name | OS Version | Role |   # CPUs   |   Cores per CPU   | Threads per Core | Peak CPU Usage |   Avg. CPU Usage   | Total RAM (GB) | Peak RAM | Ave RAM | Local Storage Total (GB) | Local Storage Usage (%) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|         |     |     |     |         |         |     |     |         |     |     |     |     |     |
|         |     |     |     |         |         |     |     |         |     |     |     |     |     |
|         |     |     |     |         |         |     |     |         |     |     |     |     |     |
|         |     |     |     |         |         |     |     |         |     |     |     |     |     |
|         |     |     |     |         |         |     |     |         |     |     |     |     |     |
|         |     |     |     |         |         |     |     |         |     |     |     |     |     |

### Virtual Servers 

Enter details below for each of the virtual servers that make up the application/workload. 

|   Hostname   | Hypervisor | OS Name | OS Version | Role |   # CPUs   |   Cores per CPU   | Threads per Core | Peak CPU Usage |   Avg. CPU Usage   | Total RAM (GB) | Peak RAM | Ave RAM | Local Storage Total (GB) | Local Storage Usage (%) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|         |     |     |     |     |         |         |     |     |         |     |     |     |     |     |
|         |     |     |     |     |         |         |     |     |         |     |     |     |     |     |
|         |     |     |     |     |         |         |     |     |         |     |     |     |     |     |
|         |     |     |     |     |         |         |     |     |         |     |     |     |     |     |
|         |     |     |     |     |         |         |     |     |         |     |     |     |     |     |
|         |     |     |     |     |         |         |     |     |         |     |     |     |     |     |

### Containers

| Container ID |   Container Name   |   Desc   |   Inbound (port)   |   Outbound (port)   |   Load Balancing (Y/N)   |   Filesystem Mounts   |   vCPU   |   Memory (MB)   |   \# Instances   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| _unique ID_ |   _web-container_   |   _User Authentication, static web content service_   |   _Load Balancer (:8443)_   |   _web-container (8443)_   |   _Y_   |   _/opt/tomcat/volumes/ccdata_   _/opt/tomcat/volumes/lucene_   |   _2.00_   |   _2460_   |   _4_   |
| _unique ID_ |   _app-container_   |   _Real-time processing of web inputs_   |   _web-container (8443)_   |   _Oracle RDS (1563)_   |   _Y_   |   _/opt/tomcat/volumes/ccdata_   _/opt/tomcat/volumes/lucene_   |   _2.00_   |   _2460_   |   _2_   |

Clusters
--------

Enter details below about the storage your application/workload currently utilizes.

| Clsuter ID |   Cluster Name   |   Description   |   # Nodes   |   Operation Mode   |   Product Name   | Product Version | VIP IP Address |
| --- | --- | --- | --- | --- | --- | --- | --- |
| unique ID |         |         |         |         |         |     |     |
|     |         |         |         |         |         |     |     |

Databases
---------

| Database ID | Database Name | Environment | Primary Usage Type | Source Engine Type | Source Engne Version | License Model | Avg IOPS | Peak IOPS | DB Size (GB) | Throughput (MBps) | Replication (Y/N) | Encryption (Y/N) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| _uniqueID_ |     | _Test,Dev,Prod_ | _OLTP/OLAP/Other_ | _Oracle, SQL, etc_ |     | _Ent, Std, etc_ |     |     |     |     |     |     |
|     |     |     |     |     |     |     |     |     |     |     |     |     |

Storage
-------

Enter details below about the storage your application/workload currently utilizes.

| Storage ID |   Type   |   Provisioned (Gb)   |   Used (Gb)   |   Max IOPS   |   Average IOPS   | Throughput (MBps) | Replication (Y/N) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| unique ID |   Local   |         |         |         |         |     |     |
|     |   NAS   |         |         |         |         |     |     |
|     |   SAN   |         |         |         |         |     |     |
|     |   Object   |         |         |         |         |     |     |

Networks
--------

Enter details about your current internet connectivity and used by the application/workload

| Network ID | Type | Provider | Description | Bandwidth (Mbps) | Peak Usage (%) | Average Usage (%) | Connection Point A | Connection Point B | Encryption (Y/N) | Encryption Method | Layer |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| _uniqueID_ | _WAN Link / VPN_ |     |     |     |     |     | _DC 1_ | _DC 2_ |     | _IPSec_ | _3_ |
| _uniqueID_ | _Internet_ |     |     |     |     |     | _DC 1_ | _Internet_ |     |     |     |

  

|   _List any specific network capability required (i.e. connections to external services or data sources)_  * * *            |  |
| --- | --- |

 **Attachments:** 


[Application%20Detailed%20Discovery%20Questionnaire.xlsx](/.attachments/DK-Portfolio/Application%20Detailed%20Discovery%20Questionnaire.xlsx)
