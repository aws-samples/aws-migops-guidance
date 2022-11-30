  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

Overview
========

The objective of application prioritization is to select the application attributes (typically 2 to 10) that will be used to establish the order in which the applications will be moved to AWS, and then assigning a corresponding score/weighting to the possible values of those attributes. Next, to define each attribute importance level for prioritization.

For example, if two attributes are being considered, such as Business Unit and Environment Type, the first step is to define the score for each possible value for those attributes. Let's assume in this example that there are three Business Units: Marketing, Retail, and Sales. Let's define what is the relative score of each of them. If the allowed scoring range is 0-100, a value in this range will be assigned to each Business Unit, let's assume 30 for Marketing, 50 for Retail, and 70 for Sales. For the Environment Type attribute, let's assume values Test, Development, and Production, with scores 20, 40, and 60 respectively. At this stage, these two attributes (Business Unit and Environment Type) will be considered equal. That means that these two attributes will influence the ranking in the same way. However, there could be cases where it is more important to prioritize based on one of them. For this example, let's assume that it is more important to prioritize based on Environment Type rather than Business Unit. The next step will be to establish Environment Type as having more importance/relevance for prioritization of applications. Depending on the tool used, the result of giving more relevance to an attribute than other is that all values of the Business Unit attribute (less important in this example), will be multiplied by a value that is less than 1 (e.g., 0.8) reducing the original score of its values and its position in the ranking. On the other hand, Environment Type (more important in this example) will be multiplied by 1, keeping its original score. This could also be achieved by changing the value score, however, when using several attributes, it could be difficult to manage each attribute. The relevance factor helps to further differentiate attributes.

**Note:** If the Discovery Tool of choice lacks the capability/features to perform application prioritization (or similar functionality), use the [MPA tool](http://mpa-proserve.amazonaws.com/) (available to AWS Employees and Partners). To use MPA, It will be required to export all application and infrastructure data from the discovery tool (or equivalent repository) and import it into MPA. Request permission from the data owner to upload their application and infrastructure data into MPA.

The result of prioritization will be a ranking of applications. If the scoring is correct, the top 20 applications should be good candidates to select from for initial migration and will be aligned to the desired criteria. If you do not generally agree with the outcome, adjust the criteria and recreate the list. It takes several iterations to obtain a baselined criteria.

Consider also the distribution of applications alongside the ranking, if too many applications (i.e., 10 or more) are clustered in the same ranking number, then review the criteria and consider using further attributes so that the result is an evenly distributed ranking with enough differentiation between small groups of workloads. Likewise, consider the complexity (e.g., number of dependencies, architecture, scale, compliance, etc.) of the applications being clustered together in the ranking. It is recommended to avoid business complex/critical applications to be migrated at the same time. Adjust the criteria so that complex applications are also evenly distributed across the ranking.

Selected attributes for pioritization
=====================================

The following table contains a base model for prioritization. This model can be used for initial prioritization during the Portfolio Discovery and Initial Planning stage in order to prioritize simple workloads. Work with the relevant stakeholders on subsequent portfolio stages to iterate and update this model and to align prioritization to business drivers.

**Notes:**

*   Add/Remove attributes if necessary.
*   The possible values require to be updated as per actual data.
*   Review and update score values.
*   If the tool being used supports prioritization of applications based on infrastructure attributes such as OS, consider adding those as High relevance with higher scoring values for cloud supported versions. 

| Attribute | Possible Values | Score | Importance/relevance |
| --- | --- | --- | --- |
| Environment | test | 60 |       High (1x)   |
| dev | 40 |
| prod | 20 |
| Regulatory Requirements | None | 60 |   High (1x)   |
| other | 10 |
|    Compliance Framework | none | 60 |       High (1x)   |
| other | 10 |
|       Business Criticality   | Low | 60 |       High (1x)   |
| Medium | 40 |
| High | 20 |
|       Number of known App to App Dependencies   | 0 | 80 |           Medium-High (0.8x)   |
| 1 | 60 |
| 2 | 40 |
| 3 or more | 20 |
| Number of Compute Instances | 1 to 3 | 60 |       Medium-High (0.8x)   |
| 4 to 10 | 40 |
| 11 or more | 20 |
| Migration Strategy (if known) | Rehost | 60 |       Medium-High (0.8x)   |
| Replaftorm | 40 |
| Refactor | 20 |
| Business Unit | (early adopters, if applicable) | 60 |   Medium-Low (0.4x)   |
| (less likely to be early adopters) | 10 |

General Guidelines for Wave 1 or Pilot Application Selection
============================================================

This is to select the ~3-5 applications that will be migrated first and help validate the Landing Zone design.

*   Web-based (accessed via web browsers)
*   2 or 3 tiered (web-app-database)
*   Apps that have no dependency (or are loosely coupled) on other applications in data center/on-prem;
*   Apps with no shared data storage (SAN/NAS) with other applications;
*   Apps that can run on AWS RDS supported databases
*   Apps with databases less than 1 TB;
*   Apps running on 2-5 server instances;
*   Preferably, stateless-architecture (can be deployed in a clustered mode using load balancer);
*   Preferably, well understood and documented architecture;
*   Can be easily rolled back;
*   Apps running a supported operating system;
*   Apps running a supported database;
*   Apps/servers running a supported license;

Applications to avoid in Wave 1 or Pilot
========================================

*   Apps serving highly available and geographically distributed e-commerce applications;
*   Data warehousing workloads;
*   ERP, CRM or Financial Reporting workloads; 
*   Middleware;
*   Workloads requiring executive-level approval for security and/or compliance;
*   Hardware/OS Examples  
    *   IBM Mainframes
        
    *   Specialized Vendor Appliances
        
    *   Solaris
        
*   Application Examples
    
    *   Information Lifecycle Management, ETL, B2B data exchanges,
        
    *   Data Warehouse
        
    *   ERPs and CRMs– SAP, PeopleSoft, Oracle ERP, Microsoft Dynamics, Siebel
        

Factors that could influence app selection for Wave 1 or Pilot
==============================================================

*   Product Release Cycle
*   Projects in-flight
*   Business criticality
*   Customer Impact
*   Buy In from Product Owner
*   QA Automation
*   Architectural Complexity
*   Application Dependencies
*   Type of dependencies – real time, transactional, batch process, etc
    
*   Allowable outage window on App
    
*   Network bandwidth/connectivity back to DC
    
*   Size of data/Storage
    
*   MSP on-boarding
    
*   Dev team in-house or outsourced
    
*   Number of server instances per application
    
*   Current License Agreements

  

Selection of Application for Wave 2 to Wave N
=============================================

Where possible, waves should be aligned to business drivers (see **Wave Planning**). Iterate the prioritization criteria so that the resulting ranking creates groups of applications where the business value of migrating them can be established and measured. For example, applications that have greater return of investment by moving them to the cloud.

References
==========

  

|   Name   |   Description   |   Link   |
| --- | --- | --- |
| AWS Prescriptive Guidance | Portfolio discovery and analysis for migration | [https://docs.aws.amazon.com/prescriptive-guidance/latest/migration-portfolio-discovery/prioritization.html](https://docs.aws.amazon.com/prescriptive-guidance/latest/migration-portfolio-discovery/prioritization.html) |

 **Attachments:** 

