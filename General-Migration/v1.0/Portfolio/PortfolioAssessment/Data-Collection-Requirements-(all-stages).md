  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

  

[[_TOC_]]

Introduction
============

  

Portfolio Assessment Data Requirements vary depending the stage. The following table specifies the minimum attributes required per stage. Use this table for socializing data requirements and update it based on the project circumstances. Combine with the **Artifact - Data Sources and Tooling Assessment**in order to match data fidelity level to data source and perform a gap analysis.

  

Business Drivers, Outcomes, and Goals are not specified in the data requirements below. However, these are considered mandatory across all stages and activities. See **Artifact - Business Drivers and Technical Guiding Principles** 

Data Requirements per Module
============================

  

**Reference:**

**Module 1:****1-Portfolio Discovery and Initial Planning**

**Module 2:****2-Prioritized Applications Assessment**

**Module 3:****3-Portfolio Analysis and Migration Planning**

**Module 4:****4-Continuous Assessment and Improvement**

  

**R = Required | O = Optional**

  

| Data Category | Attribute Name | Description | Module 1 | Module 2 | Module 3 | Module 4 | Directional Business Case | Gap Analysis |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Application** | Application ID | A unique ID. Typically available on existent CMDBs or other internal inventories and control systems. Consider creating unique IDs whenever these are not defined. | R | R | R | R | R | _35 of applications missing ID_ |
| Application Name | Application name. Including COTS vendor and product name when applicable. | R | R | R | R | R |     |
| Description | Primary application function and context | R | R | R | R | R |     |
| Environment Type | E.g., production, pre-production, development, test, sandbox | R | R | R | R | R |     |
| Migration Wave | ID or Name of the migration wave for this application | O | O | O | R | O |     |
| Business Unit |     | O | R | R | R | O |     |
| Business Owner |     | O | R | R | R | O |     |
| Criticality | High/Medium/Low E.g., strategic or revenue generating application, supporting a critical function, etc. | R | R | R | R | R |     |
| Application Type | E.g., web application, database, technical application, shared service | O | R | R | R | O |     |
| Recovery Time Objective (RTO) |     | O | R | O | R | O |     |
| Recovery Point Objective (RPO) |     | O | R | O | R | O |     |
| Availability | E.g., 365/24/7 | O | R | O | R | O |     |
| Service Level Agreement (SLA) | E.g., 99.8% | O | R | O | R | O |     |
| Revenue Generating/Strategic (Y/N) | E.g., Directly or indirectly influences company revenue | R | O | R | O | O |     |
| Location | E.g., DC1 New York | R | R | R | R | O |     |
| Users Location | E.g., US  | O | R | O | R | O |     |
| Number of Users (concurrent) | E.g., 250 | O | R | O | R | O |     |
| Release Cycle | E.g., Monthly | O | R | R | R | O |     |
| Next Release Date | Specific date | O | R | R | R | O |     |
| Maintenance Cycle | E.g., Monthly | O | R | R | R | O |     |
| Maintenance Window | E.g., Saturdays 10pm to Sunday 12pm EST | O | R | R | R | O |     |
| Migration Strategy | One of the AWS 7R's | O | R | R | R | O |     |
| Migration Considerations | Any relevant information for migration | O | R | R | R | O |     |
| Dependencies | Upstream/downstream dependencies to internal/external applications or services | O | R | R | R | O |     |
| Application Tiers | E.g., 3 (front-end, application, database) | O | R | R | R | O |     |
| Architecture Type | E.g., SOA, Monolith | O | R | R | R | O |     |
| Application Support Team | Primary support team for this application | O | R | O | R | O |     |
| Development Methodology | E.g., Agile | O | R | O | R | O |     |
| Change Control Procedures | Change control process | O | R | O | R | O |     |
| Licensing Requirements | Commodity software license type (e.g., Ms SQL Server Enterprise) | O | R | R | R | O |     |
| is COTS (Y/N) | Commercial Of The Shelf software or internal development | R | R | R | R | R |     |
| COST Vendor | E.g., IBM | O | R | R | R | R |     |
| COTS Product/Version | COTS Product and Version | O | R | R | R | R |     |
| Compliance Framework | Frameworks applicable to the workload (e.g., HIPPA, SOX, PCI-DSS, ISO, SOC, FedRAMP) | R | R | R | R | O |     |
| Regulatory Requirements | List of any regulations applicable to this workload | R | R | R | R | O |     |
| Data Sovereignty Requirements |     | R | R | R | R | O |     |
| Data Classification | PII, Public, etc | R | R | R | R | O |     |
| Monitoring Solution | How is this application monitored? specify products | O | R | O | R | O |     |
| Disaster Recovery (Y/N) |     | O | R | O | R | O |     |
| Disaster Recovery Plan | Links to existing DR Plans location | O | R | O | R | O |     |
| Software Licence Cost | Costs for software license | O | O | O | O | O |     |
| Software Operations Cost | Cost of normal operations | O | O | O | O | O |     |
| Software Maintenance Cost | Cost of scheduled maintenance | O | O | O | O | O |     |
| Target AWS Region(s) |     | O | R | O | R | O |     |
| Target AWS Account(s) # |     | O | R | O | R | O |     |
| Target AWS Service(s) | E.g., EC2, EKS, ECS, etc. | O | R | O | R | O |     |
| **Data Category** | **Attribute Name** | **Description** | **Module 1** | **Module 2** | **Module 3** | **Module 4** | **Directional Business Case** | **Gap Analysis** |
| **Infrastructure** | Unique Identifier | E.g., Asset ID. Typically available on existent CMDBs or other internal inventories and control systems. Consider creating unique IDs whenever these are not defined. | R | R | R | R | O |     |
| Asset Name | E.g., VM name, CMDB record name | R | R | R | R | O |     |
| Asset Type | E.g., Physical server, virtual server, container, virtual appliance, physical appliance, physical device, etc. | R | R | R | R | R |     |
| Hostname | Network name | R | R | R | R | O |     |
| DNS Name (FQDN) | Fully Qualified Domain Name | O | R | R | R | O |     |
| Location | E.g., DC 1 - New York | R | R | R | R | O |     |
| Description | Primary role/function | O | R | R | R | O |     |
| Environment Type | E.g., production, pre-production, development, test, sandbox | R | R | R | R | R |     |
| IP Address(es) | IP Address, preferably in <IP-Address>/<Netmask> format | O | R | R | R | O |     |
| Operating System | E.g., Windows Server | R | R | R | R | R |     |
| Operating System Major Version | E.g., 2016 | R | R | R | R | R |     |
| Licensing Requirements | Commodity license type (e.g., RHEL Standard) | O | R | O | R | O |     |
| Hypervisor | When applicable, e.g., vmware | R | R | R | R | R |     |
| State | E.g., powered on, active, inactive, powered off | R | R | R | R | R |     |
| Number of CPUs | Physical of virtual processors | R | R | R | R | R |     |
| Number of CPU Cores | Cores per processor | R | R | R | R | R |     |
| Number of CPU Threads | Threads per core | R | R | R | R | R |     |
| Total Memory | Total allocated memory | R | R | R | R | R |     |
| Attached/Local Storage Total Size | Total allocated storage space from local or attached volumes | R | R | R | R | R |     |
| Attached/Local Storage Total Used Size | Total used storage space from local or attached volumes | O | R | R | R | O |     |
| Remote Storage | E.g., NAS volumes | R | R | R | R | R |     |
| Peak CPU Usage (%) | Max usage over a period of time (typically 30 days) | O | R | R | R | O |     |
| Average CPU Usage (%) | Average usage over a period of time (typically 30 days) | O | R | R | R | O |     |
| Peak Memory Usage | Max usage over a period of time (typically 30 days) | O | R | R | R | O |     |
| Average Memory Usage | Average usage over a period of time (typically 30 days) | O | R | R | R | O |     |
| Attached/Local Storage Max IOPS | Average usage over a period of time (typically 30 days) | O | R | R | R | O |     |
| Attached/Local Storage Average IOPS | Average usage over a period of time (typically 30 days) | O | R | R | R | O |     |
| Network Max Read/Write | Max usage over a period of time (typically 30 days) | O | R | R | R | O |     |
| Network Average Read/Write | Average usage over a period of time (typically 30 days) | O | R | R | R | O |     |
| is Shared Infrastructure (Y/N) | Yes or No to denote infrastructure services that provide shared services such as authentication provider, monitoring systems, backup services, and similar services | R | R | R | R | O |     |
| Application Mapping  | Applications or application components that run in this infrastructure | O | R | R | R | O |     |
| Communication Data | E.g., server to server | O | R | R | R | O |     |
| Cost | Fully loaded costs for bare-metal servers including H/W, maintenance, operations, storage (SAN, NAS, Object), O/S license, share of rackspace, data center overheads, | O | O | O | O | R |     |
| AWS Target Region | Destination Region | O | R | O | R | O |     |
| AWS Target Account # | Destination Account | O | R | O | R | O |     |
| AWS Target Service | E.g., EC2, EKS | O | R | O | R | O |     |
| AWS Target Subnet | Subnet name | O | R | O | R | O |     |
| AWS Target Instance Type | Instance type, e.g., m5.xlarge | O | R | O | R | O |     |
| AWS Target Security Group(s) | Security Group(s) name(s) | O | R | O | R | O |     |
| AWS Target Other | Other relevant target information as needed (e.g., IAM roles) | O | R | O | R | O |     |
| **Data Category** | **Attribute Name** | **Description** | **Module 1** | **Module 2** | **Module 3** | **Module 4** | **Directional Business Case** | **Gap Analysis** |
| **Databases** | Infrastructure | Relevant attributes as per Infrastructure section | R | R | R | R | R |     |
| Primary Usage Type | E.g., OLTP, OLAP, Other | O | R | O | R | O |     |
| Source Engine Type | E.g., Oracle | R | R | R | R | R |     |
| Source Engine Version | E.g., 19.0.0.0 | R | R | R | R | R |     |
| Licensing Model | E.g., Enterprise | O | R | O | R | O |     |
| Database Size | Size of Database | R | R | R | R | R |     |
| Schemas | Number of schemas | O | R | R | R | O |     |
| Throughput | Database instance throughput, typically in MBps | O | R | O | R | O |     |
| Replication Enabled (Y/N) | Indicate existence of replicas | O | R | O | R | O |     |
| Table Partitioning (Y/N) | Indicate table partitioning | O | R | O | R | O |     |
| Encryption (Y/N) | Indicate current data encryption | O | R | O | R | O |     |
| Connection Pool | Indicates connection pool | O | R | O | R | O |     |
| Database Extensions | Indicates use of database extensions | O | R | O | R | O |     |
| SSL Support (Y/N) | Indicate use of SSL | O | R | O | R | O |     |
| AWS Target DB Engine | E.g. Oracle | O | R | O | R | O |     |
| AWS Target Other | Other relevant target information as needed | O | R | O | R | O |     |
| **Data Category** | **Attribute Name** | **Description** | **Module 1** | **Module 2** | **Module 3** | **Module 4** | **Directional Business Case** | **Gap Analysis** |
| **Storage** | Infrastructure | Relevant attributes as per Infrastructure section | R | R | R | R | R |     |
| Storage Type | E.g., NAS, Object Storage | O | R | R | R | R |     |
| Disks Type | E.g., HDD, SSD | O | R | R | R | R |     |
| Block Size (KB) | E.g., 4KB | O | O | O | O | O |     |
| Throughput (MBps) | Total throughput | O | R | O | R | O |     |
| Replication Enabled (Y/N) | Indicates volume being replicated | O | R | O | R | O |     |
| Encryption Enabled (Y/N) | Indicates encryption enabled | O | R | O | R | O |     |
| Snapshots (Y/N) | Indicate existence of regular snapshots | O | R | O | R | O |     |
| **Data Category** | **Attribute Name** | **Module 1** | **Module 1** | **Module 2** | **Module 3** | **Module 4** | **Directional Business Case** | **Gap Analysis** |
| **Networks** | Size of pipe (Mb/s), Redundancy (Y/N) | Current WAN link(s) specifications (e.g., 1000 Mb/s redundant) | O | R | R | R | R |     |
| Link Utilization | Peak and Average utilization, egress data transfer (GB/month) | O | R | R | R | O |     |
| Latency (ms) | Current latency between locations | O | R | R | R | O |     |
| Cost | Current cost per month | O | O | O | O | O |     |

 **Attachments:** 


[image2021-3-9_13-41-33.png](/.attachments/DK-Portfolio/image2021-3-9_13-41-33.png)
