  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

  

**A Word version of the Application Design and Migration Strategy template is also attached to this page (see alternative template section)**

  

[[_TOC_]]

* * *

Alternative Template
====================

The attached file contains a version of this template that can be downloaded for cases where a separate file is preferred as an alternative to confluence pages. Make sure to also download the 
 [application-diagramV2.drawio](/.attachments/DK-Portfolio/application-diagramV2.drawio)
 from this page, the diagram included within the document file cannot be edited. The same applies to the **Artifact - 7R Disposition Tree**template included in the migration strategy section of the document.

  

General Information
===================

|   Application Name   |     |
| --- | --- |
| Application ID |     |
| SDLC Environment | e.g., Production |
| Region(s) | intended target region(s) for this application |
| Number of Availability Zones |     |
| AWS Account # |     |
| Business or Technical Function | describe primary function for this application and any other secondary use case relevant to this design |
| Primary Contacts |   *   Application Owner *   Application Architect *   Enterprise Architect   |
| **Data Classification** | Public \| Non-Public \| Confidential \| Highly Confidential |
| **Service Characteristics** | Internal Facing \| External Facing  |
| Migration Strategy |   Rehost / Relocate / Replatform / Refactor or Rearchitect   |
| Migration Pattern |   Fresh install, synchronous replication, snapshot import etc.    |

Context and Problem
===================

Background
----------

*   Provide brief but relevant information so that readers have some context as to where and why the proposed changes will be made (which will be described later).
*   Assume readers are not familiar with the systems.
*   Define any needed terminology.

During discussion: Do we all understand the current state of things?

Motivation
----------

*   Why have we decided to make the proposed changes?
*   What are the benefits?
*   Will there be any downsides to the changes? Why do we think the benefits outweigh the downsides?

During discussion: Do we agree that there is strong motivation for making a change? Is there something else we have not considered?

Scope
-----

Will the solution to this problem apply to other applications/services in the portfolio? How much are we willing to generalize the solution? Declare the limits in the scope and out of scope sections.

### In Scope

*   List topics, processes, or systems that are in scope of this design

### Out of Scope

*   List anything that may be related to the design but that will not be discussed, and why.

During discussion: Do we agree that we will only stick to the in-scope topics? If not, then now is the time to bring those topics up and provide reasons for why they are relevant. For example, should this solution apply to more problems? 

  
Requirements
---------------

Document, at a high-level, the functional and non-functional requirements for this architecture.

### Functional

### Non-functional

AWS Architecture Design
=======================

This is where you describe the AWS architecture design for the application. This part can be quite long and it’s important to keep it clear and organized. The kind of organization will depend on what you are building. Unless necessary, try to keep one application per document.

Here are some tips on organization:

*   If you are making changes across multiple systems, then make a secondary heading for each system and then describe system specific changes in that section. Where possible, try to use separate documents.
*   Move any supporting material to the Appendices section.
*   If you are considering multiple approaches and technologies then document them in the Architectural Decisions table.
*   If the approach is to address the problem in multiple phases/steps, then clearly define those in the Migration Strategy section.
*   Make sure to use appropriate headings. This builds an easy to navigate outline in Confluence and makes it easier to find the right section at a glance.

_During discussion:_

1.  _Does the design make sense? Will you be able to provide support for this feature once it’s implemented and you’re on-call? Or will you be able to make changes to it?_
2.  _Is this the right design? Are there other options that are better? Are there any important downsides that make this solution not viable? Are the new APIs necessary? Do they have the right structure? Same for new data stores. Etc._
3.  _Is this architecture well-architected? (Use the AWS well architected framework)_
4.  _Is this architecture secure? Ensure security/compliance/regulatory requirements are met_

Current Application Documentation
---------------------------------

List documentation for the current implementation (on-premises, colocation, other)

| Version | Document type | Title | Links |
| --- | --- | --- | --- |
|   1.1   | design/diagram/other |         |     |
|     | infrastructure inventory |     |     |
|     | performance report |     |     |

Architectural Decisions
-----------------------

When more than one option for a given architecture has been considered, document here the options that were analyzed and the rational for selecting one of them.

| Reference ID | Architectural Pillar | Options | Rationale |
| --- | --- | --- | --- |
|   AD001   |   Security   |   *   Option A (selected) – describe option *   Option B – describe option *   Option C – describe option   | Describe motivation for selected option |

To-Be Architecture Diagram
--------------------------

Use the provided [drawio](https://app.diagrams.net/) template or provide your own. Ensure the diagram is clear and emphasizes the architectural decisions made. It is highly recommended to revisit the base template and adapt it to the specific base configuration of the Landing Zone.

Use Reference numbers in the diagram in order to link them to the Architectural Components details in the next section.

[application-diagramV2](/.attachments/DK-Portfolio/application-diagramV2.drawio)
[application-diagramV2](/.attachments/DK-Portfolio/application-diagramV2.drawio)

Architectural Component Details
-------------------------------

| Reference Number |   Logical Component Name   |   Description   |   Details   |
| --- | --- | --- | --- |
| 1 |   Internal Active Directory   |   Internal Authentication and DNS service   |   Domain will remain on-premises and will be transitioned to AWS at a later stage   |
| 2 |   External Active Directory   |   External Authentication and DNS service   |   Domain will remain on-premises and will be transitioned to AWS at a later stage   |
| 3 | Virtual Machine - ServerA | File Server | Shared Service used by multiple applications. Will remain on-premises and migrated at a later stage. |
| 4 | Virtual Machine - ServerB | File Server | Shared Service used by multiple applications. Will remain on-premises and migrated at a later stage. |
| 5 | External access | Access from external customers |   DNS servers house public and Internal DNS zones that include records for the following site:  *   api.acme.com     *   Public Routable address     *   Internally Routable address   |
| 6 | Route53 (DNS) | DNS Services in AWS |   *   Domains *   Usage   |
| 7 | KMS | EBS Volume encryption |     |
| 8 | CloudTrail | Logging and Monitoring | AWS Account activity monitoring |
|   9 / 11   | Public Subnets | Public subnet used for web services |   Subnet - Subnet ID - AZ1  Subnet - Subnet ID - AZ2   |
| 10 / 12 | NAT Gateway | Internet access for private subnets |     |
| 13 | Direct Connect | 10 Gbps link to on-premises DC 1 |     |
| 14 | Transit Gateway | Provides connectivity across VPCs and On-premises |     |
| 15 | VPC | Primary VPC | VPC ID and CIDR Range |
| 16 / 17 | Private Subnets | Private subnet used for backend servers |   Subnet - Subnet ID - AZ1  Subnet - Subnet ID - AZ2   |
| 18 / 19 | EC2 Database Instances | Database |   The primary database is deployed on an Amazon EC2 instance in one Availability Zone and a secondary database is deployed on an Amazon EC2 instance in a second Availability Zone. The databases require configuration to enable the following:  *   A highly available architecture that spans two Availability Zones      *   Async replication  *   KMS to encrypt all root and data volumes  Databased hosted on these instances:  *   Instance 1 *   Instance 2   |
| 20 | Load Balancer | Application Load Balancer |   The Load Balancer handles sticky sessions, ensuring that a single user's requests are always processed by the same backend web server. The Load Balancer works in conjunction with Auto Scaling to ensure that web requests are routed to the correct backend EC2 instance based on various factors, such as instance availability and load. The Application Load Balancer routes traffic to the auto-scaling groups.  A Security Group is used to limit access to the ALB.  *   Security Group Name:   |
| 21 / 22 | Auto Scaling Groups | Autoscaling groups are used to scale up and down according to demand |   Example: Auto Scaling provides compute resources for web services. Auto-Scaling ensures that the application can scale to accommodate various levels of application load. Additionally, Auto-Scaling is used to ensure that at least 1 instance is available at all times. The Auto Scaling group will automatically replace any instances which are terminated due to failures.  Auto Scaling Group 1 - Name - characteristics   A Security Group is used to limit access to the App Instances in the auto-scaling group.  *   Security Group Name:  Auto Scaling Group 2 - Name - characteristics   A Security Group is used to limit access to the App Instances in the auto-scaling group.  *   Security Group Name:   |
| 22 | ALB TLS Certificate | TLS Certificate used to terminate connections on the ALB |   AWS Certificate Manager is used to provision, deploy, and rotate a public TLC Certificate on the ALB. A separate wildcard TLS Certificate is used for each environment.  *   Prod: \*.acme.com *   Test: \*.test.acme.com *   Dev: \*.dev.acme.com *   Sandbox: \*.sbox.acme.com   |
| 23 / 24 | EC2 instances  | Backend services | Instance names |
| 25 | AWS Region | Region for this application | us-east-1 |

Technical Operations Components
-------------------------------

| Logical Component Name | Description | Details |
| --- | --- | --- |
| Monitoring, Alerting, Inventory, and Change Control | Monitoring, Alerting, Inventory, and Change Control |   AWS Services provide monitoring, alerting, inventory, and change control functionality.  *   CloudWatch & CloudWatch Logs *   Config & Config Rules   |
| OS Patching & Remote Access | Patching & Remove Access | AWS Systems Manager (SSM) is used to provide patching and remote access to all EC2 instances. |
| Vulnerability Scanner | Vulnerability Scanning | Amazon Inspector is used to assess applications for exposure, vulnerabilities, and deviations from best practices. After performing an assessment, Amazon Inspector produces a detailed list of security findings prioritized by level of severity. These findings can be reviewed directly or as part of detailed assessment reports which are available via the Amazon Inspector console or API. |
| Security Audit Logging | Security Audit Logging |   AWS Services provide additional security functionality.  *   CloudTrail provides Security Audit Logging *   KMS uses FIPS 140-2 validated hardware security modules to protect encryption keys used for volume and object encryption *   Secrets Manager supports the rotation, management, and retrieval of database credentials, API keys, and other secrets throughout their lifecycle   |

Security Groups
---------------

| Name / ID | Source/Destination | Protocol | Port Range | Description |
| --- | --- | --- | --- | --- |
|     |     |     |     |         |
|     |     |     |     |     |
|     |     |     |     |     |

SDLC Components
---------------

Software Development Life Cycle

| Resource | Link |
| --- | --- |
| Jira Project |   Insert link to Jira Project used to manage this application.     |
| Source Repository |   Insert link to source control repository for this application.   |
| CI/CD Pipeline Services |   AWS Services are used to store, build, and deploy infrastructure and application components through Sandbox, Dev, Test, and Prod environments.  *   CodeCommit *   CodeBuild *   CodeDeploy *   CodePipeline *   Cloudformation   |

Mandatory Tags
--------------

These tags must be added to all application resources. This list is a subset of the system-wide tags defined for the Landing Zone.

**Note**: if tagging is defined in other repositories such as MPA, then delete the table below and add the relevant link.

|   Key   |   Value   |   Description   |
| --- | --- | --- |
| Location |     | Physical location of the server |
| Organization |     | Organizational code |
| ApplicationOwner | TBD |     |
| TechnicalPOC | TBD | Technical point of contact |
| Environment | TBD | Type of environment a given device belongs to. |
| ServerType | Virtual |   Type of server.  *   EC2 instance *   Managed Service *   Container   |
| SoftwareProduct | TBD |   Software that are running on the given server.  *   JVM *   CustomApp *   CustomDB   |

Migration Strategy
==================

This is where you describe the ‘R’ Strategy chosen for this application and the associated Patterns. The R Strategy is the high-level approach (i.e., one of the 7 Rs) whilst the Pattern is the technique used to deliver the strategy. For example, an R Strategy of Refactor can utilize a Pattern of automated code refactoring with a given product or solution. Overall, this part can vary in complexity depending the path taken and It’s important to keep it clear and organized.

Here are some tips on organization:

*   Review the standard AWS R Strategy definitions (included in this document). Make sure there is a common language that AWS, Customers and Partners understands and agree to.
*   Review and update the 7R disposition tree. Include elements that are key to customer outcomes and decision-making process. The decision tree is to be used as a guide to help the customer understand the best path for an application. The outcome of an application passing through the tree can be overwritten. However, that is a good indication that tree might need to be updated.
*   Move any supporting material to the Appendix section.
*   If you are considering multiple approaches and technologies then document them in the Strategy Decisions table.
*   If the approach is to address the problem in multiple phases/steps, then clearly define those in the Strategy section.
*   Make sure to use appropriate headings. This builds an easy to navigate outline in Confluence and makes it easier to find the right section at a glance.

_During discussion:_

1.  _Does the strategy make sense? Does it align to key business drivers? Will you be able to provide support for this strategy and patterns once it’s implemented during a cut-over or migration party?_
2.  _Is this the right strategy/pattern? Are there other options that are better? Are there any important downsides that make this solution not viable?_
3.  _Has this approach been used before?_
4.  _Is this pattern secure? Ensure security/compliance/regulatory requirements are met when implementing the pattern and/or using specific tooling._

Strategy Definitions and 7R Disposition Tree
--------------------------------------------

See [7R Disposition Tree](https://myitportal.atlassian.net/wiki/spaces/PDIS27/pages/2173698378/7R+Disposition+Tree)

Strategy
--------

Document the Migration Strategy chosen for this application. Include the rationale

Patterns & Tools
----------------

Document the techniques and tools available for delivering a given Strategy. If there is more than one option available document them including the rationale for the preferred choice.

  

|   Pattern/Tool   |   Description   |   Link   |
| --- | --- | --- |
| Example: CloudEndure  | <Application components in scope of this pattern/tool> |   <APG pattern guide link>   |
|   Example: Rebuild   | <Application components in scope of this pattern/tool> | <Deployment document> |

  

Testing Considerations
----------------------

How will you ensure your changes are successful?

*   You can break up the content here into a similar structure to your design implementation such as per phase or per system.
*   Include what manual tests will be performed.

Cut-over Considerations
-----------------------

Document here any factors that need to be taken in consideration when planning for migration.

*   Cut-over dates to avoid
*   Skills required

Operational Considerations
--------------------------

How will you ensure you are ready to operate this application in AWS?

*   What kind of issues do we expect to see come up as a result of this change?

Risks, Assumptions, Issues, and Dependencies
============================================

*   What could go wrong and what will its impact be? How can we mitigate those risks?
*   Is there any risk of data corruption?
*   Are there security risks?
*   Are there performance risks?
*   What assumptions have we made?
*   What dependencies do we have to implement this architecture and migration strategy?
*   What Issues do we know about in the current implementation?
*   What issues do we expect as a result of implementing this architecture?

  

|   Type (R, A, I, D)   |   Description   |   Owner   |   Status   |
| --- | --- | --- | --- |
|     |     |     |     |
|     |     |     |     |

  

Open Questions / Parking Lot
============================

List any part of the design that we have not been able to figure out. Could be requirements or risks we don’t know how to handle or parts of other systems we’re not familiar with that can impact our design. The goal here is to acknowledge these gaps and that they will be looked into later, or possibly during the discussion if the group has ideas.

_During discussion: Is it okay to proceed with the design given that we don’t know how some things?_

  

|   Item   |   Description   |
| --- | --- |
|     |     |
|     |     |

  

Annual Run Rate Estimate
========================

| Version | Annual Total Run Rate | One Time Fee | Monthly Fee | Change | Links |
| --- | --- | --- | --- | --- | --- |
|   0.1   | $ |   $   | $ | Initial estimate |     |
|   This estimate is based on the following assumptions  (use **TCO & Annual Run Rate Estimates**to produce the estimated Run Rate)   |  |   1.  One Year Partial Upfront Reserved Instances (RIs) are used for all Production Instances 2.  Daily Change for EBS Snapshots is 0.1% 3.  Utilization for all Production instances (EC2/EBS) is 100% 4.  Utilization for all Non-Prod instances is 5 days/week at 12hrs/day 5.  Does not include Oracle Licensing 6.  Includes Sandbox, Dev, Patch, QA, and Prod environments 7.  Includes Windows OS licensing for all Windows instances 8.  Includes RHEL Licensing for all Linux instances 9.  All internal networking and security is provided by Security Groups 10.  Pricing is for AWS us-east-1 Region 11.  Includes HA and in Region DR capability   |  |  |  |

References
==========

| Name | Description | Link |
| --- | --- | --- |
| AWS Prescriptive Guidance | The AWS Prescriptive Guidance (APG) Library is a platform for authoring, reviewing, and publishing strategies, guides, and patterns. These resources are created by AWS technology specialists and APN Partners to help customers accelerate their AWS Cloud migration, modernization, and optimization projects. | [https://aws.amazon.com/prescriptive-guidance/](https://aws.amazon.com/prescriptive-guidance/) |
| AWS Well-Architected Framework | AWS Well-Architected helps cloud architects build secure, high-performing, resilient, and efficient infrastructure for their applications and workloads. Based on five pillars — operational excellence, security, reliability, performance efficiency, and cost optimization — AWS Well-Architected provides a consistent approach for customers and partners to evaluate architectures, and implement designs that can scale over time. | [https://aws.amazon.com/architecture/well-architected](https://aws.amazon.com/architecture/well-architected) |

Appendix N
==========

In general, all content should belong in a designated section.

If some content is not super relevant but may be useful to reference if desired, like a table or graph, then it can be included here. This is especially true for lengthy extra content.

 **Attachments:** 


[Application%20Design%20and%20Migration%20Strategy%20Template.docx](/.attachments/DK-Portfolio/Application%20Design%20and%20Migration%20Strategy%20Template.docx)

[application-diagramV2.drawio](/.attachments/DK-Portfolio/application-diagramV2.drawio)

[application-diagramV2.drawio.png](/.attachments/DK-Portfolio/application-diagramV2.drawio.png)
