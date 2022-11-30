  

[[_TOC_]]

Overview
========

At this stage of Portfolio Assessment it is assumed that the activities under **1-Portfolio Discovery and Initial Planning** have been completed. The Portfolio Analysis and Migration Planning stage focuses on iterating the work initiated in the previous stages aiming at enriching the portfolio data and baseline a migration wave plan.

Pre-Requisites
==============

*   Initial Application and Infrastructure Inventory
    
*   Discovery Tooling or equivalent validated sources of data
    
*   Dependency data

**Note:** if pre-requisites are not met, review and evaluate conducting activities under **1-Portfolio Discovery and Initial Planning** when necessary

Activity Details
================

| **Activity** | **Details / Guidance** | **Artifacts** |
| --- | --- | --- |
| Portfolio Analysis Party | The portfolio analysis party primary goal is to assess available data in order to initiate the construction and validation of the entire portfolio of applications (see artifact). The activities initiated during the party will be iterated in a sprint-based approach during subsequent weeks. | **3.1-Portfolio Analysis Party** |
| Iterate and baseline Application Prioritization | The default criteria in the linked artifact has been created to facilitate the prioritization of simple workloads. In this stage, iterate the criteria in parallel to the creation of the Wave Plan in order to establish a new criteria that produces a ranking of applications that is aligned to business drivers. |   **Artifact - Application Prioritization Criteria**    **Artifact - Business Drivers and Technical Guiding Principles** |
| Iterate and baseline 7R Disposition Tree  | An initial 7R Disposition Tree should be available from the **3.1-Portfolio Analysis Party** or similar workshop. The main goal of this iteration is to establish a working baseline. A baselined 7R Disposition Tree should serve as a long-term guide to define the Migration Strategy for an application or a group of applications. The baselined tree should be accurate in most cases. In some specific cases/scenarios, the strategy recommendation from the tree might be incorrect due to other factors, this is expected and the action is to overwrite the tree decision and document the rationale in the Application Migration Strategy documentation. However, consider adjusting the tree logic if this occurs in more than 15% of the cases. | **Artifact - 7R Disposition Tree** |
| Iterate and baseline Application Stacks | The Application Stacks are the result of combining Infrastructure Data with Application Data. A defined Application Stack is one that clearly describes the Application function, its key attributes, dependencies, and infrastructure (compute, storage, networks). An initial identification of Application Stacks is performed during the **3.1-Portfolio Analysis Party**. However, this work must continue until all in-scope applications have been identified. Refer to the Portfolio Analysis Party guidance and keep iterating over the remaining stacks until a baseline version of the Application and Infrastructure inventory is obtained.  At this stage, it is also expected that the chosen Discovery Tool (or equivalent source of data) has gathered information from all targeted systems. Ensure that the Infrastructure Inventory is updated with recent data and that any gaps are being actively closed. This might require manual discovery workshops.  In addition, large database states require further discovery work besides the Portfolio Parties. Conduct any specific database assessment during this stage. Consider engaging AWS specialists and specific database related offerings.   | **3.1-Portfolio Analysis Party**   **Template - Application and Infrastructure Inventory****Runbook - Database Assessment using AWS SCT**        |
| Iterate and baseline Portfolio Asset & Dependency Discovery   (Applications, Compute, Networks, Storage, Databases, Shared Services) |
| Validate Wave 1 Applications AWS Design and Migration Strategy | During Mobilize Engagements, there is a focus to migrate the first wave of applications (a.k.a. Pilot Applications). A detailed discovery/assessment of these applications, alongside an AWS Design and Migration Strategy, will be produced during the **2.1-Application Assessment Party**. Validate/Iterate the AWS Design and Migration Strategy until obtaining a baseline version for migration. Work closely with the Platform, Migration, and Operations Workstreams to achieve this goal. | **Template - Application Discovery Questionnaire****Template - Application AWS Architecture Design and Migration Strategy**   **Template - Application Migration Strategy** |
| Iterate and baseline Dependency Groups and Wave Plan | An initial Wave Plan is typically produced during the **3.1-Portfolio Analysis Party**. Follow the Wave Planning guidance and continue to iterate Dependency Groups and Wave Plans until achieving a baselined version. | **Wave Planning** |
| Evolving the Business Case | Ensure all the data collected during the Portfolio Assessment stages is incorporated into the Business Case in order to increase fidelity of its output. | **Template - Application and Infrastructure Inventory**    |

Primary Outcomes
================

1.  **Baselined Infrastructure and Application Inventory -** Inventory should include:
    
    1.  List of all VM hosts, physical and virtual servers in scope and their attributes
        
    2.  List of applications and the relevant attributes utilized for sizing, prioritization, disposition, categorization, etc.
        
    3.  Server to applications mapping
        
    4.  Server to server communication
        
    5.  Database inventory
        
    6.  Database to application mapping
        
    7.  Application to application dependency
        
2.  **Baselined 7R Disposition Tree**
    
3.  **Baselined Application Prioritization Criteria**
    
4.  **Validated AWS Design for Wave 1 or Pilot Applications**
    
5.  **Baselined Migration Wave plan**
    
    1.  MPA export
        
    2.  Other (Vendor option, modified/custom)
        
6.  **Updated Business Case**

 **Attachments:** 

