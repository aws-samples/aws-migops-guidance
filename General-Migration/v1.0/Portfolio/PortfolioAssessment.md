* * *

[[_TOC_]]

* * *

Introduction
============

**Application Portfolio Assessment** is a modular and progressive approach across all phases of the AWS Migration Framework (Assess, Mobilize, and Migrate & Modernize) developed by AWS Professional Services to discover, analyze, and plan for a portfolio of applications and IT assets moving to AWS.  It is delivered as a several sprint engagement, depending the selected modules. Throughout the modules, application and infrastructure metadata is gathered and compiled in an iterative manner in order to create deliverables and accelerate time to migration.

 ![](/.attachments/DK-Portfolio/PortfolioJourneyDetailed.png)

**Module 1**: ****1-Portfolio Discovery and Initial Planning**,** identifying existing data sources, assessing the need for discovery tooling, identifying the addressable scope and data requirements, tooling installation and configuration (if applicable), build a preliminary inventory of applications and associated infrastructure (compute, storage, networks), initial criteria for prioritization and migration strategy, identifying candidates for wave 1 (or pilot applications), and produce a directional business case (via [Migration Evaluator](https://aws.amazon.com/migration-evaluator/))  
**Module 2**: ****2-Prioritized Applications Assessment**,** prioritization of a subset of applications (e.g., wave 1 or pilot applications), initial target AWS design, migration strategy, and estimated AWS run rate for those applications.  
**Module 3**: ****3-Portfolio Analysis and Migration Planning**,** sprint based iteration to baseline a complete application/infrastructure/dependency inventory, baseline a prioritization criteria and migration strategy, and produce a high-confidence migration wave plan.   
**Module 4**: ****4-Continuous Assessment and Improvement**,** cycle/sequence of detailed Wave Assessments prior to each wave being migrated, and to iterate migration wave plans based on changing circumstances and learnings. It is also used to assess a group applications already migrated to AWS and to achieve further optimization.

 ![](/.attachments/DK-Portfolio/PortfolioJourneyHighLevel.png)

  

**Application Portfolio Assessment** is performed at two levels: 
**1/ Portfolio Level** is about collecting and analyzing general data about applications and infrastructure in order to obtain a high-level view of the entire portfolio, including technical and business aspects. This is key in order to understand priorities, the scope of the program, and to create high-confidence plans. **2/ Application Level** is about diving deep into the architecture/technology, AWS design, and migration strategy of the in-scope applications in order to perform the migration. Application Level detailed discovery is typically time consuming and it is normally done in a sequence of smaller chunks, aligned to migration waves, throughout the project lifecycle. This is the case because detailed assessment, several months in advance of target migration dates, is likely to require a new assessment closer to the actual migration date causing a repetition of activities. Therefore, detailed application level discovery is targeted at those applications that are candidates to be migrated in the near-term and then it is performed for the next chunk of applications, in sequence, throughout the project lifecycle and in parallel to ongoing migrations. The output of the Application Level discovery will be a direct input to the Platform and Migration workstreams to perform the move of applications.

The scope of work for Portfolio Assessment will depend on the program characteristics. In most cases, the Portfolio Level work + the Application Level analysis for Wave 1 (or Pilot applications) will take place during the Assess and/or Mobilize phases. Further Application Level analysis for Wave 2 to Wave n will depend on the scope and duration of the project and typically take place during the Migrate/Modernize phase.

  

Overall objectives and outcomes
===============================

*   Portfolio Discovery and Initial Planning
    *   Align with Business drivers and desired outcomes
    *   Evaluate data sources and discovery tooling
    *   Install and configure discovery tooling (if applicable)
    *   Build an initial inventory of applications and supporting infrastructure
    *   Create a directional business case
    *   Introduce default rationalization models for migration
    *   Prioritize a subset of applications for migration
*   Prioritized Applications Assessment (3-5 applications)
    *   Detailed application discovery including dependency mapping
    *   Initial AWS design
    *   Migration strategy
    *   Estimated AWS run rate
*   Portfolio Analysis and Migration Planning
    *   Complete portfolio of applications and associated infrastructure
    *   Determine application and infrastructure dependencies
    *   Customize portfolio rationalization models for migration (prioritization, and 7R's migration strategy)
    *   Migration Wave Plan
*   Continuous Assessment and Improvement
    *   Perform detailed application discovery and design elements for groups of applications (i.e., per wave)
    *   Optimization assessment for groups of workloads already migrated to AWS
    *   Wave Plan Iteration

Key Milestones
==============

*   Discovery tool selection - can existent tools/sources of data be leveraged or is a partner or AWS tool required?
*   Identify key customer (including third-parties) stakeholders to discuss application and infrastructure information (e.g., ownership, scope, strategy, requirements, outcomes).
*   Portfolio Discovery and Initial Planning
    *   Documented key business drivers
    *   Installation of required tooling (if applicable) and kick-off data collection 
    *   Obtention of application metadata
    *   Initial view of the application and infrastructure inventory completed
    *   Default portfolio rationalization models for migration established
    *   Wave 1 candidates identified
    *   Directional Business Case delivered
*   Prioritized Applications Assessment
    *   Deep dive 3-5 applications completed
    *   Initial AWS design documented
    *   AWS Migration Strategy defined
    *   AWS Run Rate estimated
*   Portfolio Analysis and Migration Planning
    *   Applications and infrastructure inventories including dependency mapping baselined
    *   Baselined portfolio rationalization models for migration (prioritization and 7R's migration strategy)
    *   Baselined migration wave plan
    *   Increased fidelity of Business Case through collected information
*   Continuous Assessment and Improvement
    *   Detailed assessment for a given wave completed
    *   Assessment of a given group of applications in AWS for further optimization completed
    *   Migration Wave plan reviewed and iterated

Risks
=====

*   Poorly defined migration scope of applications and infrastructure
*   Delays to procure, assess and install Discovery tooling (e.g., procurement, security sign-off)
*   Dependency on individuals to provide detailed application and system level details in a timely manner
*   Application owners (i.e., individuals that can make decisions on the future of the application) not identified or non-existent
*   Disruption caused by the installation or execution of an agent for discovery collection
*   Poor data collection quality (related to the discovery tool selection)
*   Incomplete identification of runtime dependencies
*   Vendor dependencies not fully understood

Early Decisions
===============

*   Is the data from the customer sufficient for a migration or does a discovery tool need to be implemented for higher fidelity data collection?
*   If discovery tooling is required, are customer security assessment required? if so, initiate those at the earliest possibility. 
*   Is the migration/modernization scope clear? is there a process defined to update scope in-flight?
*   Can a packaged offering be utilized for discovery of specific workloads (e.g., SAP, Large DB estate, Mainframe)
*   Is a survey necessary to obtain business-level information about the applications within the portfolio or can broad assumptions be made?
*   Can Licensing questions be answered and decisions made or is it necessary to perform a deeper dive into licensing (OLA/DB Freedom, etc.)?
*   Can a migration strategy be proposed and accepted or is a deeper dive into Operating Model/Business Value necessary?

  

Epics and User Stories
======================

**Note:** the epics and user stories in this template are formatted to be imported into Jira

  

 [dk-portfolioassessment_activities.csv](/.attachments/DK-Portfolio/dk-portfolioassessment_activities.csv)

Decision Backlog
================

**Note:** the user stories in this template are formatted to be imported into Jira

 [dk-portfolio_decisions.csv](/.attachments/DK-Portfolio/dk-portfolio_decisions.csv)

Public References
=================

[https://docs.aws.amazon.com/prescriptive-guidance/latest/application-portfolio-assessment-guide/introduction.html](https://docs.aws.amazon.com/prescriptive-guidance/latest/application-portfolio-assessment-guide/introduction.html)

 **Attachments:** 


[Portfolio%20Assessment%20Overview.pptx](/.attachments/DK-Portfolio/Portfolio%20Assessment%20Overview.pptx)

[PortfolioJourneyDetailed.png](/.attachments/DK-Portfolio/PortfolioJourneyDetailed.png)

[PortfolioJourneyHighLevel.png](/.attachments/DK-Portfolio/PortfolioJourneyHighLevel.png)

[dk-portfolio_decisions.csv](/.attachments/DK-Portfolio/dk-portfolio_decisions.csv)

[dk-portfolioassessment_activities.csv](/.attachments/DK-Portfolio/dk-portfolioassessment_activities.csv)
