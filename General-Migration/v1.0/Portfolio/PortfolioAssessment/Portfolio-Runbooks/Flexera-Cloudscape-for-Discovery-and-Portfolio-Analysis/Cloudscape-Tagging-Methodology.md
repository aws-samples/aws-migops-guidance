  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

Overview
--------

In the RISC Networks ITOA Platform, tags are metadata elements that are associated with assets (e.g. Windows Server) or Application Stacks. This metadata further describes the asset or application stack and can be based on collected data or external attributes. External attributes are those attributes that are known to and provided by the customer and not based on specific data points collected by the platform. The following table provides examples of each for both asset and application stack tags.

  

|   **Tag**   |   **Example**   |   **Tag Type**   |   **Based On**   |   **Comment**   |
| --- | --- | --- | --- | --- |
|   Department or Business Unit   |   IT, HR, Sales   |   Stack, Asset   |   External Data Attribute   |   Identifies which department or business unit owns the application or asset   |
|   Environment   |   Test, Dev, Prod   |   Stack, Asset   |   External Data Attribute   |   Identifies the application environment for the application or asset   |
|   RScore   |   Rehost, Replatform   |   Asset   |   Collected Data Attribute   |   Used to establish "level of effort" for a given app stack. Assets are tagged based specific criteria such as Operating System and rolled up at an application stack level   |
|   Tier   |   Web, Middleware, Database   |   Asset   |   Collected Data Attribute   |   Identifies the tier based on the existence of known web, middleware, and database processes   |

In the RISC Networks ITOA Platform, tags can be categorized as follows:

**System or default tags**

Tags that are applied and maintained in the platform by default. For more information refer to the Tags section of the glossary.

[https://portal.riscnetworks.com/app/documentation/?path=/using-the-platform/glossary/](https://portal.riscnetworks.com/app/documentation/?path=/using-the-platform/glossary/)

**DNS Tags**

Tags that are applied and maintained in the platform by default when there are licensed and accessible Windows Servers running Microsoft DNS. For more information refer to the Tags section of the glossary.

[https://portal.riscnetworks.com/app/documentation/?path=/using-the-platform/glossary/](https://portal.riscnetworks.com/app/documentation/?path=/using-the-platform/glossary/)

**Rule Based Tags**

Tags that are applied by the user based on a specific set of criteria such as Operating System or running process. In this case, the user will use the Search Applications and Processes, Advanced Rulesets, or the Assets pages in the portal to filter to a subset of assets in order to apply the appropriate tag. For example, you can tag database servers with the specific database type (MSSQL, Oracle, MySQL) running on them.

**CMDB Based Tags**

Tags that are based on external data attributes that are known to and provided by the customer. These tags are typically provided in CSV format and ultimately bulk imported into the platform using the Tag Import feature. For example, you can apply an Environment (test, dev, prod) tag to an asset or application stack.

In summary, a well thought out and implemented tagging methodology incorporates both business and technical attributes within the platform in order to gain valuable insights and make better decisions. Tags provide additional context to the assessment data and can be used directly in certain reporting modules. For example:

*   Use the Orb to see which departments share data or what portion of your environment an application owner is responsible for
*   Use the Interactive Scorecard to create a prioritized backlog of applications for migration

Rule Based Tags
---------------

The following are examples of rule based tags that can be implemented where applicable. These tags should be used wherever possible in Cloud Readiness or Cloud Migration use cases.

| Tag Key | Tag Value | Criteria | Tag Type | Comment |
| --- | --- | --- | --- | --- |
|   Migration Strategy   |   Rehost   |   Use Assets page and filter for Windows (2012, 2016, 2019), Linux (EL6, EL7)   |   Asset   |   Used to establish "level of effort" for a given app stack. Devices are tagged based on listed criteria and rolled up at an app stack level to show distribution of the different rscore tags. A device could have multiple tags depending on the approach. For example 1 tag for rehost because of OS compatibility and 1 tag for replatform because its running MySQL.   |
|   Migration Strategy   |   Replatform   |   Use Assets page and filter for Windows (2000, 2003, 2008), Linux (EL5)   |   Asset   |   Used to establish "level of effort" for a given app stack. Devices are tagged based on listed criteria and rolled up at an app stack level to show distribution of the different rscore tags. A device could have multiple tags depending on the approach. For example 1 tag for rehost because of OS compatibility and 1 tag for replatform because its running MySQL.   |
|   Migration Strategy   |   Replatform   |   Use Advanced Rulesets / Application Runpath and search for processes associated with MySQL, MSSQL, PostgreSQL, Oracle, Memcached, Redis, MongoDB etc…   |   Asset   |   Can be used to identify opportunities for moving to PaaS solutions like RDS, NoSQL (e.g. DynamoDB), Cache (Redis, Memcached) etc… This would need customer / partner input.   |
|   Database Type   |   MSSQL   |   Use Advanced Rulesets / Application Runpath and search for sqlservr.exe   |   Asset   |   Used in scorecard to identify and rank assets / application stacks with DB systems   |
|   Database Type   |   Oracle   |   Use Advanced Rulesets / Application Runpath and search for tnslsnr AND sqlplus   |   Asset   |   Used in scorecard to identify and rank assets / application stacks with DB systems   |
|   Database Type   |   MySQL   |   Use Advanced Rulesets / Application Runpath and search for mysqld   |   Asset   |   Used in scorecard to identify and rank assets / application stacks with DB systems   |
|   Database Type   |   PostgreSQL   |   Use Advanced Rulesets / Application Runpath and search for postgres   |   Asset   |   Used in scorecard to identify and rank assets / application stacks with DB systems   |
|   Cloud Criteria   |   Cluster   |   Use Advanced Rulesets / Application Context and search for Microsoft Cluster Services   |   Asset   |   Used in scorecard to identify and rank assets / application stacks with running HA solutions   |
|   Cloud Criteria   |   NFS Mount   |   Use Advanced Rulesets / Filesystem and search for NFS   |   Asset   |   Used in scorecard to identify and rank assets / application stacks with NFS mounts   |

CMDB Based Tags
---------------

The following are examples of CMDB based tags that can be used where available and / or applicable. These tags are typically provided in CSV format and bulk imported into the platform using the Tag Import feature.

| Tag Key | Example Tag Value | Tag Type | Comment |
| --- | --- | --- | --- |
|   Application Classification / Application Categorization   |   Enterprise Resource Management, Operations Management, Data Management, Security   |   Stack   |   Identifies the type of application   |
|   Department / Business Unit   |   IT, HR, Sales   |   Stack, Asset   |   Identifies which department or business unit owns the application or asset   |
|   Supported By   |   Business, Outsourced   |   Stack, Asset   |   Support Organization, Department, or Individual   |
|   Environment   |   Test, Dev, Prod   |   Stack, Asset   |   Identifies the application environment for the application or asset   |
|   Data Type   |   HIPPA, PII, PCI-DSS   |   Stack   |   Identifies if application data is subject to compliance requirements   |
|   Application Criticality   |   Mission Critical, Mission Essential, Tactical   |   Stack   |   Identifies the criticality of the application to the business   |
|   Application Name   |   SharePoint, CRM, Cognos   |   Asset   |   Import of CMDB info (application to server mapping) for reference   |
|   Datacenter / Location   |   US-Virginia   |   Asset   |   Datacenter or Location designation   |
|   In-Scope   |   Yes, No   |   Asset   |   Used to flag devices in the Inaccessible Device list that are not in scope and / or flag devices that will be licensed   |
|   Support SLA   |   Gold, Silver, Bronze   |   Stack   |   Identifies support SLA for the application   |
|   RTO/RPO   |   4h / 24h   |   Stack   |   Recovery Time Objective, Recovery Point Objective - Used in Disaster Recovery and Business Continuity planning   |
|   Application Lifecycle / Status   |   Deploy, Maintain, Retire, End of Support   |   Stack   |   Identifies the lifecycle stage or overall status for the application stack   |
|   Migration Wave   |   Wave 1   |   Stack   |   If customer has already authored a wave strategy incorporate into portal   |
|   Business Disposition   |   Retain, Replace, Refactor,Retire   |   Stack, Asset   |   Business decision for the disposition of application stack or asset   |
|   Application Module   |   Access Management, Portal, Integration, EDI, Front-End   |   Asset   |   Modular server role for associated application   |

Examples
--------

### Migration Strategy

The follow illustrates how to create Rehost and Replatform tags based on Operating System version. A general rule of thumb is that if the Operating System version is still under mainstream support it would be considered a Rehost. Whereas if the Operating System version has gone End of Support (EOS) it would be considered a Replatfom. There is some nuance here and ultimately this will be based on the customer's preference and priorities.

1.  Navigate to the **Consume Intelligence** >> **Assets** page
2.  Filter the OS Version column for "2016" to filter down to Microsoft Windows Server 2016 based systems
3.  Maximize the number of records per page (e.g. 100)
4.  Click to check the box in the header row to select all filtered systems
5.  Click on Manage Tags
6.  Type "Migration Strategy" in for the Tag Key and Create New Tag
7.  Type Rehost for the Tag Value
8.  Apply Tag

 ![](/.attachments/DK-Portfolio/worddav18130ffba5a5b7a3d8f1b19668ae246a.png)

1.  If there were more than 100 results then advance to the next page and apply the same tag
2.  Repeat this process for other OS Versions to assign Rehost or Replatform tag values as necessary

### Database Type

The follow illustrates how to create a Database Type tag that can be used to understand database distribution in the customer environment and opportunities to leverage Platform as a Service (PaaS) solution offerings.

#### Microsoft SQL Server

1.  Navigate to **Add Intelligence** >> **Advanced Rulesets**
2.  Click Add New Rule
3.  Set rule for Application Runpath, Contains, sqlservr.exe

 ![](/.attachments/DK-Portfolio/worddave81a22f196bac9689d1af3733a020901.png)

1.  Add rule
2.  Click on (select) newly created rule to list result in table below
3.  Shift select all rows
4.  Right click >> Manage Tags
5.  Enter "Database Type" for Tag Name and "MSSQL" for Tag Value
6.  Apply Tag

#### Oracle

1.  Navigate to **Add Intelligence** >> **Advanced Rulesets**
2.  Click Add New Rule
3.  Set rule for Application Runpath, Contains, tnslsnr

 ![](/.attachments/DK-Portfolio/worddav730a254d1270776df037a8a9beab81ce.png)

1.  Add rule
2.  Click on (select) newly created rule to list result in table below
3.  Shift select all rows
4.  Right click >> Manage Tags
5.  Enter "Database Type" for Tag Name and "Oracle" for Tag Value
6.  Apply Tag

* * *

 **Attachments:** 


[worddav18130ffba5a5b7a3d8f1b19668ae246a.png](/.attachments/DK-Portfolio/worddav18130ffba5a5b7a3d8f1b19668ae246a.png)

[worddav730a254d1270776df037a8a9beab81ce.png](/.attachments/DK-Portfolio/worddav730a254d1270776df037a8a9beab81ce.png)

[worddavd1e96de8791df7162744a1c3357aadbb.png](/.attachments/DK-Portfolio/worddavd1e96de8791df7162744a1c3357aadbb.png)

[worddave81a22f196bac9689d1af3733a020901.png](/.attachments/DK-Portfolio/worddave81a22f196bac9689d1af3733a020901.png)
