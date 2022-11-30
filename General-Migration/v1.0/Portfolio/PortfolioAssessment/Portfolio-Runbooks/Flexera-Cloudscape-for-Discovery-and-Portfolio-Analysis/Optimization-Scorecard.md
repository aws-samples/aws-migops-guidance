  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

Overview
========

This document will provide guidance and best practices around using the RISC Networks ITOA Platform, and specifically the Optimization Scorecard, to support Cloud Readiness and Cloud Migration use cases.

Assumptions and Pre-requisites
==============================

The following outlines the assumptions and pre-requisites that this document and the guidance contained herein are based on.

*   You must have a healthy assessment and follow all general best practices and standard processes that apply. This includes, but is not limited to, the following:
    *   All in-scope assets must be fully discovered and accessible (i.e. Device Type of Windows Server, Virtual-Windows Server, Generic Server, or Virtual-Generic Server)
    *   All in-scope assets must be licensed and successfully collecting data (Summary of Collection dashboard)
    *   All in-scope assets must be organized and placed into Application Stacks that represent the customers environment in a manner that is aligned with the overall project goals
*   You must determine and implement a tagging methodology / approach that will support the customers requirements and reflect the business and technical goals of the Cloud base initiative.

Customer Input (Tags)
=====================

The following types of data can be incorporated into the platform as tags. This allows incorporation of external attributes, or “soft data”, into Cloud Readiness or Cloud Migration decision criteria. The table below provides an example list of possible tags. Each customer will likely have a different set of priorities based on the specifics of their environment. For example, the customer may need to evacuate a specific location or data center before lease expiration. In this case location may be a primary factor in prioritization. Other customers may prioritize applications that are owned by infrastructure teams for the initial set of migrations.

| Tag Key | Example Tag Value | Tag Type | Comment |
| --- | --- | --- | --- |
|   Department / Business Unit   |   IT, HR, Sales   |   Stack, Asset   |   Identifies which department or business unit owns the application or asset   |
|   Supported By   |   Business, Outsourced   |   Stack, Asset   |   Support Organization, Department, or Individual   |
|   Environment   |   Test, Dev, Prod   |   Stack, Asset   |   Identifies the application environment for the application or asset   |
|   Data Type   |   HIPPA, PII, PCI-DSS   |   Stack   |   Identifies if application data is subject to compliance requirements   |
|   Application Priority   |   Mission Critical, Mission Essential, Tactical   |   Stack   |   Identifies the criticality of the application to the business and inherent risk associated with migration   |
|   Datacenter / Location   |   US-Virginia   |   Asset   |   Datacenter or Location designation   |
|   Application Lifecycle / Status   |   Deploy, Maintain, Retire, End of Support   |   Stack   |   Identifies the lifecycle stage or overall status for the application stack   |
|   Business Disposition   |   Retain, Replace, Refactor,Retire   |   Stack, Asset   |   Business decision for the disposition of application stack or asset   |
|   Risk   |   High, Medium, Low   |   Stack   |   Business disposition of application in terms on overall risk. Is application stack well known / documented, is it revenue producing, etc..   |

  
Rule Based Tags

Migration Strategy (rscore)
---------------------------

The RISC Networks ITOA Platform provides a default set of rscore tags that can be incorporated into Cloud suitability or migration decision criteria. The default set of rscore tags, and the rule logic behind them are documented within the glossary.

[https://portal.riscnetworks.com/app/documentation/?path=/using-the-platform/glossary/](https://portal.riscnetworks.com/app/documentation/?path=/using-the-platform/glossary/)

Because every customer can have a slightly different set of priorities, it is recommended that customers create a customized rscore or Migration Strategy tag. For example, some customers may want to prioritize opportunities to replatform based on the PaaS offerings of the Cloud provider in order to take advantage of the operational efficiencies and scale that these services provide. Other customers may choose to standardize on a minimum OS level as part of a migration effort. In this case the following approach can be used, and modified as needed, to support a custom rscore or Migration Strategy tag.

| Tag Key | Tag Value | Criteria | Tag Type | Comment |
| --- | --- | --- | --- | --- |
|   Migration Strategy   |   Rehost   |   Use Assets page and filter for Windows (2012, 2016, 2019), Linux (EL6, EL7)   |   Asset   |   Used to establish "level of effort" for a given app stack. Devices are tagged based on listed criteria and rolled up at an app stack level to show distribution of the different rscore tags. A device could have multiple tags depending on the approach. For example 1 tag for rehost because of OS compatibility and 1 tag for replatform because its running MySQL.             |
|   Migration Strategy   |   Replatform   |   Use Assets page and filter for Windows (2000, 2003, 2008), Linux (EL5)   |   Asset   |
|   Migration Strategy   |   Refactor or Replatform   |   Use Assets page and filter for AIX, HPUX, or Solaris   |   Asset   |
|   Migration Strategy   |   Replatform or Replatform-PaaS   |   Use Advanced Rulesets / Application Runpath and search for processes associated with MySQL, MSSQL, PostgreSQL, Oracle, Memcached, Redis, MongoDB etc…   |   Asset   |   Can be used to identify opportunities for moving to PaaS solutions like RDS, NoSQL (e.g. DynamoDB), Cache (Redis, Memcached) etc… This would need customer / partner input.   |

Cloud Criteria
--------------

There are many factors that indicate an applications readiness for Cloud migration and the level of effort required to migrate it. For example, applications that use shared NFS file systems may require special consideration to determine how to support this shared storage dependency in the Cloud. File system data can be migrated to AWS EFS or the application can be reconfigured to use AWS S3. For this miscellaneous set of criteria, we can implement a Cloud Criteria tagging methodology. The following table includes examples of this tagging methodology.  

| Tag Key | Tag Value | Criteria | Tag Type | Comment |
| --- | --- | --- | --- | --- |
|   Cloud Criteria   |   Cluster   |   Use Advanced Rulesets / Application Context and search for Microsoft Cluster Services   |   Asset   |   Used to identify assets / application stacks with running HA solutions   |
|   Cloud Criteria   |   NFS Mount   |   Use Advanced Rulesets / Filesystem and search for NFS   |   Asset   |   Used to identify assets / application stacks with NFS mounts   |

Tag Consumption        
=======================

Now that we have thought through and implemented a tagging methodology the question becomes “now what?”. How can these tags be leveraged to support the desired outcome?

On a basic level the tags and tag values can be consumed in several places within the platform. For example, you can view device and stack level tags from the View Individual Application Stack (VIAS) page thus providing additional context when reviewing an application with the Application Owner. Device tags can be viewed in the Server table and the Tag Distribution option can be used to visualize the tag value composition of that stack. In other words, does the stack have multiple tiers, is it completely rehostable or are there replatform elements as well. Lastly, stack level tags are included in the VIAS summary report.

The Consume Intelligence >> Application Classification page provides a way to visualize how the tag values are distributed across the environment at a high level. For example, you can visualize the customers use of different Database systems (MSSQL, Oracle, MySQL, etc.) when filtering on the Database Type tag assuming it was implemented.  

The remainder of this document will focus on using these tags in the context of the Optimization Scorecard.

Optimization Scorecard
======================

The Migration Scorecard provides an automated way to rank your application stacks for Cloud migration priority based on criteria of your choosing. The Migration Scorecard can also be used to rank for Cloud readiness or other use cases depending on the criteria used and how each criterion is weighed. This document will focus on creating a prioritized list of applications for migration.

Example - RISC Basic Scorecard
------------------------------

We will start with a basic use of the scorecard to establish rank and prioritization of application stacks. This basic approach will incorporate standard criterion that should exist in any assessment. The following table describes the criteria that can be used, and the associated weight applied.

|   **Category**   |   **Tag Key**   |   **Tag Value**   |   **Weight**   |
| --- | --- | --- | --- |
|   Predictive Cloud Run Cost   |   NA   |   NA   |   50   |
|   Low Connectivity   |   NA   |   NA   |   75   |
|   Low Device Count   |   NA   |   NA   |   30   |
|   Small Storage Footprint   |   NA   |   NA   |   30   |
|   Device Tags   |   Rscore or Migration Strategy   |   Rehost   |   60   |

Example - RISC Advanced Scorecard
---------------------------------

A more advanced use of the scorecard will incorporate customer input and rule-based tags for a broader approach to establishing rank and prioritization of application stacks. The following table describes the criteria that can be used and the associated weight applied.

|   **Category**   |   **Tag Key**   |   **Tag Value**   |   **Weight**   |
| --- | --- | --- | --- |
|   Predictive Cloud Run Cost   |   NA   |   NA   |   50   |
|   Low Connectivity   |   NA   |   NA   |   75   |
|   Low Device Count   |   NA   |   NA   |   30   |
|   Small Storage Footprint   |   NA   |   NA   |   30   |
|   Device Tags   |   Rscore or Migration Strategy   |   Rehost   |   60   |
|   Device Tags   |   Environment   |   Test, Development, QA   |   50   |
|   Stack Tags   |   Risk   |   Low   |   75   |
|   Stack Tags   |   Risk   |   Medium   |   60   |

 **Attachments:** 

