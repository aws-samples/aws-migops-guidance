  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

  

Overview
========

In order to identify the sources of data, it is key to understand the**Data Collection Requirements (all stages)**. Data collection processes can take a significant amount of time and easily become a blocker when there is no clarity about what data is needed when. The key is to understand the balance between what is too little and what is too much data for the outcomes of the current stage. Adopting a progressive approach to data collection permits to focus on the data and the level of fidelity that is necessary to meet the current requirements.

Start with identifying the key stakeholders that can fulfil the data requirements, these are typically members of Service Management, Operations, Capacity Planning, Monitoring, Application Owners, and Support Teams. The approach is to establish working sessions with members of these groups, socialize data requirements, and obtain an indicative list of tools and existing documentation that can provide those data.

Assessment Questions
====================

Alternative Template
--------------------

The attached file can be downloaded and used as an alternative to the questionnaire in this confluence page. It contains the same questionnaire.

 [Data%20Sources%20and%20Tooling%20Assessment%20Questionnaire.xlsx](/.attachments/DK-Portfolio/Data%20Sources%20and%20Tooling%20Assessment%20Questionnaire.xlsx)

This questionnaire is to be used in early conversations when assessing existing Data Sources and Discovery Tooling options for Application Portfolio Assessment.

Questionnaire
-------------

### How accurate and up to date is the infrastructure and application inventory?

Please note if active discovery tools and processes are utilized to keep the CMDB updated, if not please specify the last date of data refresh.  Attach a copy of the inventory in a format as close as possible to the **Template - Application and Infrastructure Inventory** template with this completed questionnaire.

### Does your inventory contain application to infrastructure mapping?

### Does your inventory contain dependency data?

Note the existence of communication data such as server to server, application to application, application/server to database

### What tools that can provide application and infrastructure information are available in your environment?

Note the existence of performance, monitoring, and management tools that could be used as a source of discovery data

### Please provide the name(s) of your data centers (Name and Location)

### Are your servers and/or applications operated by a third party?

### What is the high-level process for gaining approval to deploy discovery tools?

If infrastructure inventory data is not already available, credentials will be required to collect this data from your infrastructure (e.g., containers, virtual/physical servers, hypervisors, databases). If so, what's the high-level process and timeframe for gaining approval?

### What is the main authentication process to access infrastructure such as servers, containers and databases? Are server credentials local or centralized? What is the process to obtain credentials?

Obtaining credentials for the discovery tool to connect to each asset can be challenging, especially when these are not centralized

### What is the network security zones outline? can you provide a network diagram?

### What is the process for requesting firewall rules in your data centers?

### What are the current support SLA’s in relation to data center operations (discovery tool installation, firewall requests)?

### Please provide the main point-of-contact and contact information for each area defined below:

| Area | Point-of-contact name | Point-of-contact email address |
| --- | --- | --- |
| Project Management Office |     |     |
| Cloud COE |     |     |
| Information Security |     |     |
| Compliance |     |     |
| Owner of CMDB |     |     |
| Head of Infrastructure |     |     |
|   Data Center Operations   |     |     |
| Networking |     |     |
|   Databases  *   SQL *   Oracle *   Other   |     |     |
| Windows  |     |     |
| Linux |     |     |
| Finance |     |     |
| Communications |     |     |
| Training |     |     |
| Other |     |     |

  

Data Sources Assessment
=======================

Once these questions have been answered, list the identified sources of data and proceed to assign a level of fidelity (or level of trust) to each of them. Recently validated data (i.e., 0-30 days) from active programmatic sources, such as tools, have the highest level of fidelity. Static data, such as documents, workbooks, manually updated CMDBs, or any other non-programatically maintained data set, or whose last refresh date is older than 60 days, are considered of lower fidelity and are less trusted.

The data fidelity levels in the table below are indicative, assess the requirements of the program in terms of the maximum tolerance to assumptions and associated risk in order to determine what is an appropriate level of fidelity. Proceed to update the table below based on your analysis.  
  
Data fidelity:  

| Data Sources | Fidelity Level | Rationale | Portfolio coverage | Comments |
| --- | --- | --- | --- | --- |
| _Tribal Knowledge (\*)_ | _Low_ | _Up to 25% of accurate data, 75% assumed values or data is older than 150 days_ | _Low_ | _Scarce, focused on critical applications._ |
| _Knowledge Base_ | _Medium-Low_ | _Up to 35-40% of accurate data, 65-60% assumed values or data is 120-150 days old._ | _Medium_ | _Manually maintained. Inconsistent levels of detail._ |
| _CMDB_ | _Medium_ | _~50% of accurate data, ~50% assumed values or data is 90-120 days old._ | _Medium_ | _Contains data from mixed sources. Several data gaps._ |
| _VMware vCenter exports_ | _Medium-High_ | _Up to 75-80% of accurate data, 25-20% assumed values or data is 60-90 days old._ | _High_ | _Covers 90% of the virtualized estate_ |
| _Application Performance Monitoring (APM)_ | _High_ | _Mostly accurate data, ~5% assumed values or data is 0-60 days old._ | _Low_ | _Limited to critical production systems (covers 15% of the application portfolio)_ |

(\*) Tribal Knowledge refers to any information about applications and infrastructure that is not documented.

Once the current data sources have been identified, the recommendation is to gather information from as many systems as possible. This approach has the benefit of helping to update the current portfolio view and what is known about applications and infrastructure. It also helps to make progress when there is no clarity about what is targeted to move. The recommended approach is to review existing data (e.g., CMDB outputs, ITSM systems) and construct a list of assets targeted for data collection. If there is clarity of what is in scope and out of scope of migration you might restrict data collection to those systems in scope.

There could be situations in which there is uncertainty about which applications or servers are in a given data center or source location. In these cases, obtaining bare metal and hypervisor lists from existent management tools will be helpful. For example, connecting to hypervisors permits to obtain lists of virtual machines to be targeted for data collection.

Note that the initial output, when combining existing data sources, is likely to be incomplete. The key is to perform a gap analysis in terms of **Data Collection Requirements (all stages)**and what can be obtained from existing sources. It is important to contrast % of completeness with level of data fidelity. Higher completeness levels from low fidelity sources will contain several assumptions that could lead to invalid analysis. Whilst early stages of assessment do not require the maximum data fidelity, it is still recommended that data sources are at least medium to medium-high fidelity. Contrast these numbers against risk tolerance and the use of assumptions to fill data gaps.

The gap analysis will help you understand the quantity and quality of data you are working with and to establish the level of assumptions that need to be made in order to move forward. Discovery tooling can help to fill the gaps and collect high fidelity data. The next section contains guidelines to evaluate for discovery tooling. It is recommended to deploy discovery tooling at the earliest possibility in order to increase the confidence levels in data and accelerate migration outcomes. Also, to accelerate readiness when internal procurement, security, and implementation processes for new tools requires several weeks/months to complete.

Evaluating Discovery Tooling
============================

Does your organization need discovery tooling? Portfolio assessment requires high-confidence, up-to-date data about applications and infrastructure. Initial stages of portfolio assessment can use assumptions to fill data gaps. However, as progress is made, high-fidelity data enables the creation of successful migration plans and the correct estimation of target infrastructure to reduce cost and maximize benefits. It also reduces risk by enabling implementations that consider dependencies and avoids migration pitfalls. The primary use case for discovery tooling in cloud migration programs is to reduce risk and increase confidence levels in data through the following:

*   Automated or programmatic data collection, resulting in validated, highly trusted data
*   Acceleration of the rate at which data is obtained, improving project speed and reducing costs
*   Increased levels of data completeness, including communication data and dependencies not typically available in CMDBs
*   Obtaining insights such as automated application identification, TCO analysis, projected run rates, and optimization recommendations
*   High-confidence migration wave planning

  
When there is uncertainty about whether systems exist in a given location, most discovery tools can scan network subnets and discover those systems that respond to ping or Simple Network Management Protocol (SNMP) requests. Note that not all network or systems configurations will allow ping or SNMP traffic. Discuss these options with networks and technical teams.

Further stages of application portfolio assessment and migration heavily rely on accurate dependency-mapping information. Dependency mapping provides an understanding of the infrastructure and configuration that will be required in AWS (such as security groups, instance types, account placement, and network routing). It also helps with grouping applications that must move at the same time (such as applications that must communicate over low latency networks). In addition, dependency mapping provides information for evolving the business case.

When deciding on a discovery tool, it is important to consider all stages of the assessment process and to anticipate data requirements. Data gaps have the potential to become blockers, so it is key to anticipate those by analyzing future data requirements and data sources. Experience in the field dictates that most stalled migration projects have a limited dataset in which the applications in scope, associated infrastructure, and their dependencies are not clearly identified. This lack of identification can lead to incorrect metrics, decisions, and delays. Obtaining up-to-date data is the first step to successful migration projects.

How to select a discovery tool?
-------------------------------

Several discovery tools in the market provide different features and capabilities. Consider requirements and decide on the most appropriate option for this program. The most common factors when deciding on a discovery tool for migrations are the following:

**Security**

*   What is the authentication method to access the tool data repository or analytics engines?
*   Who can access the data, and what are the security controls to access the tool?
*   How does the tool collect data? Does it need dedicated credentials?
*   What credentials and access level does the tool need to access my systems and obtain data?
*   How is data transferred between the tool components?
*   Does the tool support data encryption at rest and in-transit?
*   Is data centralized in a single component inside or outside of my environment?
*   What are the network and firewall requirements? Ensure that security teams are involved in early conversations about discovery tooling.  
    

**Data sovereignty**

*   Where is the data stored and processed?
*   Does the tool use a software as a service (SaaS) model?
*   Does it have the possibility to retain all data within the boundaries of my environment?
*   Can data be screened before it leaves the boundaries of my organization? Consider your organization needs in terms of data residency requirements.  
    

**Architecture**

*   What infrastructure is required and what are the different components?
*   Is more than one architecture available?
*   Does the tool support installing components in air-locked security zones?  
    

**Performance**

*   What is the impact of data collection on my systems?

**Compatibility and scope**

*   Does the tool support all or most of my products and versions? Review the tool documentation to verify supported platforms against the current information about your scope.
*   Are most of my operating systems supported for data collection? If you don’t know your operating system versions, try to narrow the list of discovery tools to those with the wider range of supported systems.  
    

**Collection methods**

*   Does the tool require to install an agent on each targeted system?
*   Does it support agent-less deployments?
*   Do agent and agent-less provide the same features?
*   What is the collection process?  
    

**Features**

*   What are the features available?
*   Can it calculate total cost of ownership (TCO) and estimated AWS Cloud run rate?
*   Does it support migration planning?
*   Does it measure performance?
*   Can it recommend target AWS infrastructure?
*   Does it perform dependency mapping?
*   What level of dependency mapping does it provide? Consider tools with strong application and infrastructure dependency-mapping functions and those that can infer applications from communication patterns.  
    

**Cost**

*   What is the licensing model?
*   How much does the licensing cost?
*   Is the pricing for each server? Is it tiered pricing?
*   Are there any options with limited features that can be licensed on-demand? Discovery tools are typically used throughout the entire lifecycle of migration projects. If your budget is limited, consider at least 6 months. However, absence of discovery tooling typically leads to higher manual effort and internal costs.  
    

**Support model**

*   What levels of support are provided by default?
*   Is any support plan available?
*   What are the incident response times?  
    

**Professional services**

*   Does the vendor offer professional services to analyze discovery outputs?
*   Can they cover the elements of this guide?
*   Are there any discounts or bundles for tooling + services?

  

Use the [Discovery Tool Comparison guide](https://aws.amazon.com/prescriptive-guidance/migration-tools/migration-discovery-tools/) to find and evaluate discovery tooling.

Recommended features for the discovery tool
-------------------------------------------

To avoid provisioning and combining data from multiple tools over time, a discovery tool should cover the following minimum features:

*   **Software** – The discovery tool should be able to identify running processes and installed software.
*   **Dependency mapping** – It should be able to collect network connection information and build inbound and outbound dependency maps of the servers and running applications. Also, the discovery tool should be able to infer applications from groups of infrastructure based on communication patterns.
*   **Profile and configuration discovery** – It should be able to report the infrastructure profile such as CPU family (for example, x86, PowerPC), the number of CPU cores, memory size, number of disks and size, and network interfaces.
*   **Network storage discovery** – It should be able to detect and profile network shares from network-attached storage (NAS).
*   **Performance** – It should be able to report peak and average utilization of CPU, memory, disk, and network.
*   **Gap analysis** – It should be able to provide insights on data quantity and fidelity.
*   **Network scanning** – It should be able to scan network subnets and discover unknown infrastructure assets.
*   **Reporting** – It should be able to provide collection and analysis status.

Additional features to consider
-------------------------------

*   **TCO analysis** – It should be able to provide a cost comparison between current on-premises cost and projected AWS cost.
*   **Licensing analysis and optimization recommendations** – It should be able to identify and analyze Microsoft SQL Server and Oracle systems to identify current licensing and AWS optimization for rehost and replatform scenarios.
*   **Migration strategy recommendation** – The discovery tool should be able to make default migration R type recommendations based on current technology.
*   **Inventory export** (to CSV or a similar format)
*   **Right-sizing recommendatio**n (for example, can it map a recommended target AWS infrastructure?)
*   **Dependency visualization** (for example, can dependency mapping be visualized in a graphical mode?)
*   **Architectural view** (for example, can architectural diagrams be automatically produced?)
*   **API access** (for example, can it be programmatically accessed to refresh data on your CMDB?)
*   **Application prioritization** (can it assign weight or relevance to application and infrastructure attributes to create prioritization criteria for migration?)
*   **Wave planning** (for example, recommended groups of applications and the ability to create migration wave plans)
*   **Migration cost estimation** (estimation of effort to migrate)

Deployment considerations
-------------------------

After you have selected and procured a discovery tool, consider the following questions to drive conversations with the teams responsible for deploying the tool in your organization:

*   Are servers or applications operated by a third party? This could dictate the teams to involve and processes to follow.
*   What is the high-level process for gaining approval to deploy discovery tools?
*   What is the main authentication process to access systems such as servers, containers, storage, and databases? Are server credentials local or centralized? What is the process to obtain credentials? Credentials will be required to collect data from your systems (for example, containers, virtual or physical servers, hypervisors, and databases). Obtaining credentials for the discovery tool to connect to each asset can be challenging, especially when these assets are not centralized.
*   What is the network security zones outline? Are network diagrams available?
*   What is the process for requesting firewall rules in the data centers?
*   What are the current support service-level agreements (SLAs) in relation to data center operations (discovery tool installation, firewall requests)?

 **Attachments:** 


[Data%20Sources%20and%20Tooling%20Assessment%20Questionnaire.xlsx](/.attachments/DK-Portfolio/Data%20Sources%20and%20Tooling%20Assessment%20Questionnaire.xlsx)
